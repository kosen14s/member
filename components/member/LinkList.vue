<template>
  <div class="link-list">
    <ul>
      <li class="link-box" v-show="links.site_url">
        <a :href="links.site_url">
          <img class="link-icon" src="~/assets/images/logos/site_mono.png" alt="site">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/site.png" alt="site">
        </a>
      </li>
      <li class="link-box" v-show="links.twitter_id">
        <a :href="'https://twitter.com/'+ links.twitter_id">
          <img class="link-icon" src="~/assets/images/logos/twitter_mono.png" alt="twitter">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/twitter.png" alt="twitter">
        </a>
      </li>
      <li class="link-box" v-show="links.facebook_id">
        <a :href="'https://www.facebook.com/'+ links.facebook_id">
          <img class="link-icon" src="~/assets/images/logos/facebook_mono.png" alt="facebook">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/facebook.png" alt="facebook">
        </a>
      </li>
      <li class="link-box" v-show="links.instagram_id">
        <a :href="'https://www.instagram.com/'+links.instagram_id">
          <img class="link-icon" src="~/assets/images/logos/instagram_mono.png" alt="instagram">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/instagram.png" alt="instagram">
        </a>
      </li>
      <li class="link-box" v-show="links.github_id">
        <a :href="'https://github.com/'+ links.github_id">
          <img class="link-icon" src="~/assets/images/logos/github_mono.png" alt="github">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/github.png" alt="github">
        </a>
      </li>
      <li class="link-box" v-show="links.tumblr_id">
        <a :href="'https://'+links.tumblr_id+'.tumblr.com'">
          <img class="link-icon" src="~/assets/images/logos/tumblr_mono.png" alt="tumblr">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/tumblr.png" alt="tumblr">
        </a>
      </li>
      <li class="link-box" v-show="links.blog_url">
        <a :href="links.blog_url">
          <img class="link-icon" src="~/assets/images/logos/blog_mono.png" alt="blog">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/blog.png" alt="blog">
        </a>
      </li>
      <li class="link-box" v-show="links.youtube_url">
        <a :href="links.youtube_url">
          <img class="link-icon" src="~/assets/images/logos/youtube_mono.png" alt="youtube">
          <img class="link-icon link-icon-hover" src="~/assets/images/logos/youtube.png" alt="youtube">
        </a>
      </li>
    </ul>
  </div>
</template>

<script>
  export default {
    props: ["links"],
    data(){
      return {
      }
    }
  }
</script>
<style lang="scss">
@import '~assets/styles/normalize.scss';
@import '~assets/styles/variables.scss';
@import '~assets/styles/mixin.scss';
.link-list{
  display: inline-block;
  padding-top: 4px;
  .link-box {
    margin: 0;
    padding: 0;
    a {
      display: block;
      position: relative;
      width: auto;
      height: auto;
      .link-icon {
        width: 40px;
        height: 40px; //54px以上でロゴ使用権利範囲内
        transition: .3s ease-out;
        opacity: 1;
        filter:brightness(80%);
        transform: scale(1);
      }
      .link-icon-hover {
        position: absolute;
        top: 0;
        left: 0;
        opacity: 0;
        transition: .3s ease-out;
        filter:brightness(100%);
        transform: scale(1);
      }
      &:hover {
        .link-icon {
          opacity: 0;
          transform: scale(1.2);
        }
        .link-icon-hover {
          opacity: 1;
          transform: scale(1.2);
        }
      }
    }
  }
}
@media(max-width: 1350px) {
  .link-list{
    .link-box {
      a {
        .link-icon {
          width: 38px;
          height: 38px; //54px以上でロゴ使用権利範囲内
        }
      }
    }
  }
}
</style>
