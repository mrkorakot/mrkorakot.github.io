<template lang="pug">
  .bodyInner
    character
    nuxt
</template>

<script>
import character from '~/components/character.vue'

export default {
  components: {
    character
  }
}
</script>

<style lang="scss">
  @import "~assets/styles/layout.scss";
</style>
