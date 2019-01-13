<template lang="pug">
  .container.member
    ul.member_list
      li(v-for="member in filteredView" :key="member.id").member_list_item
        img(:src="`https://raw.githubusercontent.com/kosen14s/member/master/icons/${member.icon}`" :alt="'icon'").back-icon
        div.member_list_item_wrapper
          .member-header
            img(:src="`https://raw.githubusercontent.com/kosen14s/member/master/icons/${member.icon}`" :alt="'icon'").member-icon
            .member-name
              h2 {{member.name}}
              LinkList(:links="member.links")

          .contents.origin-box(v-if="detail")
            p.origin(v-if="member.origin") {{member.origin}}

          .contents.area-box(v-if="detail")
            p.property-name(v-if="member.area") 生息地：
            p.property(v-if="member.area") {{member.area}}

          .self-info-box(v-if="detail")
            p.property-name コメント：
            p(v-for="selfinfo in member.self_introduction" :key="selfinfo.id").self-info {{selfinfo}}

          ChannelList(:channels="member.channels" :season="season" v-on:addchanneltag="addChannelTag" v-if="detail")
      .more-display(v-if="filteredView.length<this.filter.search_hit && filteredView.length>0")
        button(@click="filter.display = filter.display+6") さらに表示

    div(v-if="filteredView.length==0 && load==true") フィルタリングの結果、ヒットしませんでした。
</template>
<script>
  import LinkList from '~/components/member/LinkList.vue'
  import ChannelList from '~/components/member/ChannelList.vue'

  export default {
    props: ["filter","members","detail","season"],
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
            console.log(this.filter.search.toLowerCase());
            var search_text = this.filter.search.toLowerCase();
            var self_intro_txt = "";
            var channeltag_link = 0;
            var origin = "";
            var area = "";

            if(member.self_introduction != null){
              for (var j in member.self_introduction) {
                self_intro_txt = self_intro_txt + member.self_introduction[j];
              }
            }
            if(member.channels != null){
              for (var j in member.channels){
                if(this.filter.channeltags.indexOf(member.channels[j]) !== -1){
                  channeltag_link++;
                }
              }
            }
            if(member.origin != null){
              origin = member.origin;
            }
            if(member.area != null){
              area = member.area;
            }
            if((member.name.toLowerCase().indexOf(search_text) !== -1 ||
              origin.toLowerCase().indexOf(search_text) !== -1 ||
              area.toLowerCase().indexOf(search_text) !== -1 ||
              self_intro_txt.toLowerCase().indexOf(search_text) !== -1)
              && (channeltag_link==this.filter.channeltags.length)) {
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
      border-radius: 0;
      padding: 10px;
      width: 31.4%;
      position: relative;
      .back-icon {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        z-index: -1;
        filter: opacity(30%) blur(20px);
      }
      .member_list_item_wrapper{
        padding-bottom: 16px;
        z-index: 0;
      }
      .member-header {
        padding-top: 12px;
        display:flex;
        flex-wrap: nowrap;
        .member-icon {
          width:80px;
          height:80px;
          border: 1px solid #fff;
          background-color: #fff;
          border-radius: 20px;
          margin-right: 20px;
        }
        .member-name{
          padding-top: 8px;
          h2 {
            font-size: 2.4rem;
            margin: 0;
            display: block;
            padding-left: 8px;
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
