<template>
  <div>
    <nuxt/>
  </div>
</template>

<style lang="scss">
@import '~assets/styles/normalize.scss';
@import '~assets/styles/variables.scss';
@import '~assets/styles/mixin.scss';

html {
  font-size: 62.5%;
  height: 100%;
  font-family: $noto-font;
}
body {
  width: 100%;
  height: 100%;
  margin: 0;
  position: relative;
  background-color: white;
  font-size: 1.8rem;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #222;
}
::selection {
  background: $member-def;
  color: white;
}
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 4px;
}
a {
  color: $member-def;
  text-decoration: none;
}
p {
  margin: 1rem 0;
  font-size: 1.8rem;
  line-height: 2.8rem;
}
.container {
  width: 1500px;
  margin:auto;
}
@media(max-width: 1600px) {
  :root {
    --section: 94%;
  }
  .container {
    margin: 0 calc((100% - var(--section)) / 2) 0;
    width: var(--section);
  }
}
</style>
