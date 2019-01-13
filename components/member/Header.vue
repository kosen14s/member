<template lang="pug">
  div
    header(:style="'background-color:'+season.color")
      .container
        .title
          a(href="https://kosen14s.github.io").sub-title
            img(src="~/assets/images/kosen14s_logo.png" alt="logo")
            h2 kosen14s 
              span TOP
          h1 #profile
        p.discription kosen14sのメンバーのうち、{{members.length}}人が自己紹介を書いてくれました。
        .display-detail
          button(v-show="detail == true" @click="$emit('display-detail')") 詳細を閉じる
          button(v-show="detail == false" @click="$emit('display-detail')") 詳しく表示

</template>

<script>
  export default {
    props:["members","detail","season"],
  }
</script>

<style lang="scss">
@import '~assets/styles/normalize.scss';
@import '~assets/styles/variables.scss';
@import '~assets/styles/mixin.scss';

header {
  background-color: #fff;
  color: white;
  padding: 32px 0 18px;
  position: relative;
  transition: .5s ease-out;
  .title {
    a.sub-title {
      display: inline-flex;
      flex-wrap: nowrap;
      transition: .1s ease-out;
      color: white;
      &:hover{
        opacity: .7;
      }
      img {
        width: 28px;
        height: 28px;
      }
      h2 {
        line-height: 28px;
        margin: 0;
        padding-top: 2px;
        padding-left: 8px;
        font-size: 1.7rem;
        span {
          font-size: 2rem;
        }
      }
    }
    h1 {
      margin: 1.2rem 0 .8rem;
      font-size: 4rem;
    }
  }
  .discription {
    font-size: 1.6rem;
  }
  .display-detail {
    position: absolute;
    bottom: 8px;
    right: 0;
    button {
      @include inputbutton;
      background: white;
      transition: .3s ease-out;
      cursor: pointer;
      color: black;
    }
  }
}
@media(max-width: 1000px) {
  header {
    .display-detail {
      position: initial;
      text-align: right;
      margin: 0 calc((100% - var(--section)) / 2) 0;
    }
  }
}
</style>
