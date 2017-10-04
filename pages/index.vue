<template lang="pug">
  .mainContent(
    :id="page"
  )
    .intro(
      ref="intro"
    )
      .items
        .item
        .item
    character(
      :active="characterActive"
    )
</template>

<script>
import character from '~/components/character.vue'
import {TimelineLite, TweenLite, Elastic, Power4} from 'gsap'
export default {
  name: 'Home',
  data () {
    return {
      page: 'home',
      characterActive: false
    }
  },
  head: {
    title: 'Mr.Korakot Suppol'
  },
  components: {
    character
  },
  methods: {
    introAnimated () {
      this.characterActive = true
    }
  },
  mounted () {
    const thisComp = this
    const $intro = this.$refs.intro
    const tl = new TimelineLite({
      onComplete () {
        thisComp.introAnimated()
      }
    })
    tl.add(TweenLite.from($intro, 1, {
      width: 100,
      ease: Power4.easeIn
    }))
    tl.add(TweenLite.from($intro, 2, {
      rotation: 45,
      ease: Elastic.easeOut
    }))
  }
}
</script>

<style lang="scss">
  @import "~assets/styles/intro.scss";
</style>