<template lang="pug">
  div
    section.filter
      .container
        .search-box
          input(v-model="filter.search" placeholder="キーワード検索").filter-search
          button(@click="filter.display=6").filter-display 6人表示
          button(@click="filter.display=12").filter-display 12人表示
        .filter-view
          ul(v-show="filter.channeltags.length").filter-tag-box
            li(v-for="channeltag in filter.channeltags" :key="channeltag.id").channel
              button(@click="removeChannelTag(channeltag)").channel_button {{"# "+channeltag}}
            button(@click="removeAllTag").channel_button.channel_button_delete ×

          .filter-current-status
            p {{this.filter.member_viewlength}} / {{this.filter.search_hit}}人表示
</template>

<script>
  export default {
    props: ["filter"]
  }
</script>

<style lang="scss">
.filter {
  margin-top: 8px;
  .search-box {
    .filter-search {
      font-family: "Noto Sans Japanese";
      font-size: 1.4rem;
      line-height: 2rem;
      border: 1px solid #a3c0b9;
      border-radius: 5px;
      padding: 4px 8px 6px;
      color: #222;
      transition: .3s ease-out;
      &::placeholder {
        color: #a3c0b9;
      }
      &:focus {
        outline:none;
        color: white;
        border-color:#4c9689;
        background: #4c9689;
      }
    }
    .filter-display {
      font-family: "Noto Sans Japanese";
      font-size: 1.4rem;
      line-height: 2rem;
      background: white;
      border: 1px solid #a3c0b9;
      border-radius: 5px;
      padding: 4px 8px 6px;
      color: #222;
      transition: .3s ease-out;
      cursor: pointer;
      &:focus {
        outline:none;
      }
      &:hover{
        border-color:#4c9689;
        background: #4c9689;
        color: white;
      }
    }
  }
  .filter-view {
    .filter-tag-box{
      margin: 4px 0;
      display: inline-block;
      padding-right: 24px;
    }
    .filter-current-status {
      font-size: 1.4rem;
      margin: 10px 0;
      p {
        margin: 0;
      }
    }
  }
}
</style>
