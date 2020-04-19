<template>
  <div id="app">
    <v-header></v-header>
  </div>
</template>

<script>
import VHeader from 'components/v-header/v-header'

export default {
  name: 'App',
  components: {
    VHeader
  }
}
</script>

<style lang="stylus">
#app
  // position fixed
  // top 136px
  // left 0
  // right 0
  // bottom 0
</style>
