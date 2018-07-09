<template>
  <li>
    <h2><a v-bind:href="a.url" target="_blank">{{ a.name }}</a></h2>
    <img :src="a.image[2]['#text']" />
  </li>
</template>

<script>
export default {
  name: 'artist',
  props: ['a']
}
</script>

<style lang="stylus">
li
  display block
  maring 10px 0
</style>

