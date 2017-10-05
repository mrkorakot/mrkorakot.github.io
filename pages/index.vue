<template lang="pug">
  .mainContent(
    :id="page"
  )
    .intro(
      ref="intro"
    )
      .introEffect(
        ref="introEffect"
      )
        .items(
          v-if="effectShow"
        )
          .item(
            v-for="index in 5"
            ref="effectItem"
          )
    character(
      :active="characterActive"
    )
</template>

<script>
import character from '~/components/character.vue'
import {TimelineLite, Elastic, Power4} from 'gsap'
export default {
  name: 'Home',
  data () {
    return {
      page: 'home',
      characterActive: false,
      effectShow: false
    }
  },
  head: {
    title: 'TEST'
  },
  components: {
    character
  },
  methods: {
    introAnimate () {
      var thisComp = this
      var $intro = thisComp.$refs.intro
      var tl = new TimelineLite({
        onComplete () {
          thisComp.introAnimated($intro)
        }
      })
      tl.from($intro, 1, {
        width: 100,
        ease: Power4.easeIn
      }).from($intro, 2, {
        rotation: 45,
        ease: Elastic.easeOut
      })
    },
    introAnimated ($intro) {
      $intro.classList.add('done')
      this.characterActive = true
      this.effectShow = true
      this.$nextTick(function () {
        this.introEffectAnimate()
        setInterval(() => this.introEffectAnimate(), 10000)
      })
    },
    introEffectAnimate () {
      var thisComp = this
      var $effects = thisComp.$refs.effectItem
      var tl = new TimelineLite({
        onComplete () {
          thisComp.introEffectAnimated()
        }
      })
      var top = 0
      var overlap = 0
      var duration = 1
      var height = 10
      for (let $effect of $effects) {
        top = Math.floor((Math.random() * 200) + 1)
        overlap = Math.random()
        duration = Math.floor((Math.random() * 2) + 1)
        height = Math.floor(Math.random() * (15 - 5 + 1)) + 5
        tl.from($effect, duration, {
          'margin-top': -top,
          left: -200,
          width: 200,
          height: height,
          ease: Power4.easeIn
        }, '-=' + overlap)
      }
    },
    introEffectAnimated () {

    }
  },
  mounted () {
    this.introAnimate()
  }
}
</script>

<style lang="scss">
  @import "~assets/styles/intro.scss";
</style>