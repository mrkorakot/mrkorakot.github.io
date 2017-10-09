<template lang="pug">
  transition(
    name="character"
    v-on:after-enter="afterEnter"
  )
    .character(
      :class="{'active': active}"
      v-if="characterShow"
      ref="character"
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
        this.$emit('actived')
        this.$nextTick(() => this.dynamicShadow())
      },
      dynamicShadow () {
        const character = this.$refs.character
        let raf = ''
        let start = {
          x: 0,
          y: 0
        }
        function lerp (start, end) {
          const dx = end.x - start.x
          const dy = end.y - start.y

          return {
            x: start.x + dx * 0.1,
            y: start.y + dy * 0.1
          }
        }
        document.addEventListener('mousemove', (e) => {
          const end = {
            x: ((e.clientX / window.innerWidth) - 0.5) * 2,
            y: ((e.clientY / window.innerHeight) - 0.5) * 2
          }
          start = lerp(start, end)
          raf = raf || requestAnimationFrame(update)
        })
        function update () {
          character.style.setProperty('box-shadow', (start.x * -15) + 'px' + ' ' + (start.y * -15) + 'px 20px rgba(0,0,0,0.5)')
          character.style.setProperty('--x', start.x)
          character.style.setProperty('--y', start.y)
          raf = null
        }
      }
    },
    mounted () {
    }
  }
</script>

<style lang="scss">
  @import "~assets/styles/transition.scss";
  @import "~assets/styles/character.scss";
</style>