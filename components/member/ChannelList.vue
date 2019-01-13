<template>
  <div class="contents channels" v-if="channels.length!=0">
    <p class="property-name">お気に入りチャンネル：</p>
    <ul class="property">
      <li v-for="channel in channels" :key="channel.id" class="channel">
        <button @click="$emit('addchanneltag', channel)" class="channel_button">{{"# "+channel}}</button>
      </li>
    </ul>
  </div>
</template>
<script>
  export default {
    props: ["channels","channeltags"],
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
  .channel {
    display: inline-block;
    margin: 0;
  }
  .channel_button {
    @include inputbutton;
    background: $member-def;
    border: none;
    transition: .3s ease-out;
    cursor: pointer;
    &:hover {
      background: $member-def-light;
    }
  }
  .channel_button_delete {
    background: #864242;
    &:hover {
      background: #b36565;
    }
  }

</style>

