<template lang="pug">
  .mainContent(
    :id="page"
  )
    .loadingIndicator(
      v-if="loadingIndicatorShow"
      ref="loadingIndicator"
      :class="{'done':loadingIndicatorDone}"
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
            img(src="~static/img/bike-view-top.svg" width="307" height="438")
    character(
      :characterShow="characterShow"
      @actived="charcterActived"
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
      loadingIndicatorDone: false
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
      var width = 100
      var random = 0
      for (let $effect of $effects) {
        random = Math.random()
        top = Math.floor((random * 200) + 1)
        overlap = Math.floor(random * (2 - 1 + 1)) + 1
        duration = Math.floor(random * (5 - 1 + 1)) + 1
        width = Math.floor(random * (width - 40 + 1)) + 40
        tl.to($effect, 0, {
          'margin-top': -top,
          'width': width
        }).from($effect, duration, {
          'left': 0,
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
    },
    charcterActived (e) {
      this.$nextTick(function () {
        this.introEffectAnimate()
      })
    }
  },
  mounted () {
    // setTimeout(() => {
    //   this.loadingIndicatorDone = true
    //   this.$nextTick(function () {
    //     this.loadingIndicatorAnimateOut()
    //   })
    // }, 5000)
  }
}
</script>

<style lang="scss">
  @import "~assets/styles/intro.scss";
  @import "~assets/styles/loadingIndicator.scss";
</style>