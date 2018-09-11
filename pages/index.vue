<template lang="pug">
  div
    <Header :members="members" :detail="detail" @display-detail="toggleDetail"/>
    section.filter
      .container
        .search-box
          input(v-model="filter.search" placeholder="キーワード検索").filter-search
          //- button(@click="filter.display=6").filter-display 6人表示
          //- button(@click="filter.display=12").filter-display 12人表示
          ul(v-show="filter.channeltags.length").filter-tag-box
            li(v-for="channeltag in filter.channeltags" :key="channeltag.id").channel
              button(@click="removeChannelTag(channeltag)").channel_button {{"# "+channeltag}}
            button(@click="removeAllTag").channel_button.channel_button_delete ×
        .filter-current-status
          p Filtering result :  {{this.filter.search_hit}} 人
          p Display :  {{this.filter.member_viewlength}} 人

    <MemberList :filter="filter" :members="members" :detail="detail" @filtered-data="filteredData"/>
</template>

<script>
import axios from 'axios'
import fetch from 'node-fetch'
import Header from '~/components/member/Header.vue'
import MemberList from '~/components/member/MemberList.vue'

export default {
  layout: 'member',
  components: {
    Header,
    MemberList
  },
  data() {
    return {
      filter: {
        display: 12,
        search: "",
        search_hit:0,
        member_viewlength:0,
        channeltags: [],
        all_channel_list: []
      },
      members: [],
      detail: true
    }
  },
  methods: {
    removeChannelTag(channeltag) {
      for (let i = 0; i < this.filter.channeltags.length; i++) {
        if(this.filter.channeltags[i] == channeltag){
          this.filter.channeltags.splice(i, 1);
        }
      }
    },
    removeAllTag() {
      this.filter.channeltags=[];
    },
    filteredData(data) {
      this.filter.search_hit = data.hit
      this.filter.member_viewlength = data.memlength
    },
    toggleDetail() {
      if(this.detail==true){
        this.detail=false
      }else{
        this.detail=true
      }
    }
  },
  // asyncData({}) {//わからん
  //   axios.get(`https://kosen14s.github.io/member/json/members.json`)
  //     .then((res) => {
  //       console.log(res.data)
  //       return { members : res.data }
  //     })
  // },
  created: function() {
    fetch('https://raw.githubusercontent.com/kosen14s/member/master/members.json')
      .then(res => res.json())
      .then(json => {
        this.members = json
      })
  }
}
</script>

<style lang="scss">
@import '~assets/styles/normalize.scss';
@import '~assets/styles/variables.scss';
@import '~assets/styles/mixin.scss';

.filter {
  margin-top: 8px;
  .search-box {
    .filter-search {
      font-family: $noto-font;
      @include inputbutton;
      border: 1px solid $member-def-lightgray;
      color: #222;
      transition: .3s ease-out;
      &::placeholder {
        color: $member-def-lightgray;
      }
      &:focus {
        outline:none;
        color: white;
        border-color: $member-def;
        background: $member-def;
      }
    }
    .filter-display {
      font-family: $noto-font;
      font-size: 1.3rem;
      line-height: 1.8rem;
      background: white;
      border: 1px solid $member-def-lightgray;
      border-radius: 5px;
      padding: 3px 8px;
      margin: 0 2px;
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
  .filter-tag-box {
    margin: 0;
    display: inline-block;
    //ChannelList.vue
  }
  .filter-current-status {
    margin: 5px 0;
    p {
      display: inline-block;
      font-size: 1.4rem;  
      margin: 0;
      &:last-child {
        padding-left: 20px;
      }
    }
  }
}
</style>

