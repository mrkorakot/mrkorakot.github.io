<template lang="pug">
  .mainContent(
    :id="page"
  )
    .loadingIndicator(
      v-if="loadingIndicatorShow"
      ref="loadingIndicator"
      :class="{active:loadingIndicatorActive}"
    )
      .items
        .item(v-for="index in 2")
    .intro(
      v-if="introShow"
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
      :characterShow="characterShow"
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
      effectShow: false,
      introShow: false,
      characterShow: false,
      loadingIndicatorShow: true,
      loadingIndicatorActive: false
    }
  },
  head: {
    title: 'TEST'
  },
  components: {
    character
  },
  watch: {
    introShow (val) {
      if (val) {
        this.$nextTick(function () {
          this.introAnimate()
        })
      }
    }
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
        width: 80,
        ease: Power4.easeIn
      }).from($intro, 2, {
        rotation: 0,
        ease: Elastic.easeOut
      })
    },
    introAnimated ($intro) {
      $intro.classList.add('done')
      this.characterShow = true
      this.effectShow = true
      this.$nextTick(function () {
        this.introEffectAnimate()
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
        tl.to($effect, 0, {
          'margin-top': -top
        }).from($effect, duration, {
          left: 0,
          height: height,
          ease: Power4.easeIn
        }, '-=' + overlap)
      }
    },
    introEffectAnimated () {
      this.introEffectAnimate()
    },
    loadingIndicatorAnimateOut () {
      var thisComp = this
      var $block = thisComp.$refs.loadingIndicator
      var tl = new TimelineLite({
        onComplete () {
          thisComp.introShow = true
        }
      })
      tl.to($block, 1, {
        rotation: 90,
        ease: Power4.easeIn
      }).to($block, 1, {
        width: '100%'
      })
    }
  },
  mounted () {
    setTimeout(() => {
      this.loadingIndicatorActive = true
      this.$nextTick(function () {
        this.loadingIndicatorAnimateOut()
      })
    }, 5000)
  }
}
</script>

<style lang="scss">
  @import "~assets/styles/intro.scss";
  @import "~assets/styles/loadingIndicator.scss";
</style>