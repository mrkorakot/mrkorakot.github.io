<template lang="pug">
  .character(
    :class="{'active': active}"
  )
    .characterInner {{ title }}
      .image
        img
      .caption
        .captionInner
          .titleText
            div Lorem ipsum dolor sit amet,
            div consectetur adipisicing elit.
          .desc
            div Nesciunt ipsam delectus,
            div natus reiciendis itaque quos unde ducimus.
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
        console.log('charcter active! = ', val)
      }
    },
    methods: {
    }
  }
</script>

<style lang="scss">
  @import "~assets/styles/character.scss";
</style>