<template>
  <div>
    <router-link :to="{ name: 'index' }">Index</router-link>
    <h1 v-html="title"/>
    <div v-html="body"/>
    <img :src="img"/>
  </div>
</template>

<script>
import Stack from '~/plugins/entry'
import axios from 'axios'

export default {
  async asyncData() {
    let res = await Stack.getEntry('technology', 'blt74c9a141281d9f99')

    return { entry: res, body: res.technology_description, title: res.technology_title, img: res.technology_image }
  }
}
</script>

<style>

</style>
