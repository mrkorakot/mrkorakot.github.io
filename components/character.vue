<template lang="pug">
  .character(
    :class="{'active': active}"
  )
    .characterInner {{ title }}
      .image
        img
</template>
<script>
  export default {
    name: 'character',
    data () {
      return {
        title: 'TEST'
      }
    },
    props: [
      'active'
    ],
    watch: {
      active (val) {
        console.log(val)
      }
    },
    methods: {
    }
  }
</script>

<style lang="scss">
  @import "~assets/styles/character.scss";
</style>