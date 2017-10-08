<template lang="pug">
  transition(
    name="character"
    v-on:after-enter="afterEnter"
  )
    .character(
      :class="{'active': active}"
      v-if="characterShow"
    )
      .characterInner
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
        title: 'TEST',
        active: false
      }
    },
    props: [
      'characterShow'
    ],
    watch: {

    },
    methods: {
      afterEnter () {
        this.active = true
      }
    }
  }
</script>

<style lang="scss">
  @import "~assets/styles/transition.scss";
  @import "~assets/styles/character.scss";
</style>