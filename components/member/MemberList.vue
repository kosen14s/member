<template lang="pug">
  .container.member
    ul.member_list
      li(v-for="member in filteredView" :key="member.id").member_list_item
        div
          .member-header
            .member-color
            img(:src="`https://raw.githubusercontent.com/kosen14s/member/master/icons/${member.icon}`" :alt="'icon'").member-icon
            .member-name
              h2 {{member.name}}
              <LinkList :links="member.links"/>

          .contents.origin-box(v-show="detail")
            p.origin(v-show="member.origin") {{member.origin}}

          .contents.area-box(v-show="detail")
            p.property-name 生息地：
            p.property(v-show="member.area") {{member.area}}

          .self-info-box(v-show="detail")
            p.property-name コメント：
            p(v-for="selfinfo in member.self_introduction" :key="selfinfo.id").self-info {{selfinfo}}

          <ChannelList :channels="member.channels" v-on:addchanneltag="addChannelTag" v-show="detail"/>
      .more-display(v-show="filteredView.length<this.filter.search_hit && filteredView.length>0")
        button(@click="filter.display = filter.display+6") さらに表示

    div(v-show="filteredView.length==0") フィルタリングの結果、ヒットしませんでした。
</template>
<script>
  import LinkList from '~/components/member/LinkList.vue'
  import ChannelList from '~/components/member/ChannelList.vue'

  export default {
    props: ["filter","members","detail"],
    data(){
      return {
      }
    },
    components: {
      LinkList: LinkList,
      ChannelList: ChannelList
    },
    methods: {
      addChannelTag(channeltag){
        if (this.filter.channeltags.indexOf(channeltag) == -1){//既存のtagに存在しなければ追加
          this.$parent.filter.channeltags.push(channeltag);
        }else{
          for (let i = 0; i < this.filter.channeltags.length; i++) {//既存のtagに存在してたら削除
            if(this.filter.channeltags[i] == channeltag){
              this.filter.channeltags.splice(i, 1);
            }
          }
        }
      }
    },
    computed: {
      filteredView() {
        var seachmembers = [];
        var display_vol = this.filter.display-1
        var hit = 0;

        for (var i in this.members) {
            var member = this.members[i];
            var self_intro_txt = "";
            var channeltag_link = [];

            for (var j in member.self_introduction) {
                self_intro_txt = self_intro_txt + member.self_introduction[j];
            }
            for (var j in member.channels){
              if(this.filter.channeltags.indexOf(member.channels[j]) !== -1){
                channeltag_link.push(true);
              }
            }
            if((member.name.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1 ||
              member.origin.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1 ||
              member.area.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1 ||
              self_intro_txt.toLowerCase().indexOf(this.filter.search.toLowerCase()) !== -1)
              && (channeltag_link.length==this.filter.channeltags.length)) {
              if(display_vol >= hit){
                seachmembers.push(member);
              }
              hit++;
            }
        }
        this.$emit('filtered-data', {hit: hit , memlength: seachmembers.length} )
        //this.$parent.filter.search_hit = hit;
        //this.$parent.filter.member_viewlength = seachmembers.length;
        return seachmembers;
      }
    }
  }
</script>
<style lang="scss">
@import '~assets/styles/normalize.scss';
@import '~assets/styles/variables.scss';
@import '~assets/styles/mixin.scss';
.member {
  ul.member_list {
    display: flex;
    flex-wrap: wrap;
    li.member_list_item {
      margin: 4px;
      padding: 36px;
      border-radius: 0;
      width: 28%;
      .member-header {
        padding-top: 12px;
        display:flex;
        flex-wrap: nowrap;
        position: relative;
        .member-color {
          position: absolute;
          top: -18px;
          left: 0;
          right: 0;
          margin: auto;
          width: 100%;
          height: 1px;
          background-color: #999;
        }
        .member-icon {
          width:80px;
          height:80px;
          border: 1px solid #ddd;
          border-radius: 20px;
          margin-right: 20px;
        }
        .member-name{
          h2 {
            font-size: 2.4rem;
            margin: 0;
            display: block;
          }
        }
      }
      .contents {
        display: flex;
        flex-wrap: wrap;
        margin: 0;
      }
      .property-name {
          font-size: 1.2rem;
          line-height: 2.6rem;
          display: block;
          color: #58615f;
          margin: 0;
        }
      .property {
        display: inline-flex;
        flex-wrap: wrap;
        font-size: 1.5rem;
        line-height: 2.6rem;
        margin: 0;
        width: auto;
        padding-left: .5rem;
      }
      .origin-box {
        margin-top: 1.4rem;
        .origin {
          display: inline-flex;
          flex-wrap: wrap;
          font-size: 1.6rem;
          line-height: 2.6rem;
          margin: 0;
          width: auto;
        }
      }
      .area-box {
        margin-top: .5rem;
      }

      .self-info-box {
        margin: 1.5rem 0;
        .self-info_property {
          font-size: 1.2rem;
          line-height: 2rem;
          display: block;
          color: #333;
          margin: 1.5rem 0 0;
        }
        .self-info {
          margin: 0 0 .5rem;
          font-size: 1.4rem;
          line-height: 2rem;
          padding-left:1rem;
        }
      }
    }
    .more-display {
      width: 100%;
      text-align: center;
      margin-bottom: 200px;
      button {
        margin: 20px;
        width: 200px;
        font-family: "Noto Sans Japanese";
        font-size: 1.6rem;
        line-height: 50px;
        background: #ecf0ef;
        border: none;
        border-radius: 5px;
        color: #222;
        transition: .3s ease-out;
        cursor: pointer;
        &:focus {
          outline:none;
        }
        &:hover{
          border-color: $member-def;
          background: $member-def;
          color: white;
        }
      }
    }
  }
}
@media(max-width: 1600px) {
  .member {
    ul.member_list {
      li.member_list_item {
        margin: 0.2%;
        padding: 2%;
        width: 28.93%;
      }
    }
  }
}
@media(max-width: 1200px) {
  .member {
    ul.member_list {
      li.member_list_item {
        .member-header {
          display: inline-block;
          .member-name{
            margin-top: 8px;
          }
        }
      }
    }
  }
}
@media(max-width: 1000px) {
  .member {
    ul.member_list {
      li.member_list_item {
        padding: 2%;
        margin: 0.3%;
        width: 45.4%;
        .member-header {
          display: flex;
          .member-color {
            top: -12px;
          }
          .member-name{
            margin-top: 0;
          }
          .member-icon {
            width:30%;
            height:30%;
            border: 1px solid #ddd;
            border-radius: 10%;
            margin-right: 5%;
          }
        }
      }
    }
  }
}
@media(max-width: 640px) {
  .member {
    ul.member_list {
      li.member_list_item {
        padding: 6% 2%;
        margin: 2px 0;
        width: 100%;
        .member-header {
          .member-color {
            top: -8px;
          }
        }
      }
    }
  }
}
</style>
