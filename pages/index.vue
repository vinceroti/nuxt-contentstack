<template>
  <div>
    <router-link :to="{ name: 'testpage' }">test</router-link>
    {{ time() }} - testing cache
    <div v-html="bio"/>
    <div class="flex-container">
      <img :src="img.src" v-for="(img, key) in imgdata.items" :key="key"/>
    </div>
  </div>
</template>

<script>
import Stack from '~/plugins/entry'
import axios from 'axios'

export default {
  serverCacheKey () {
    return Math.floor(Date.now() / 1000000) //need this for server caching
  },
  async asyncData() {
    let res = await Stack.getEntry('team_members', 'blt3ec29586cf35b4d6')
    let imgdata

    try {
      imgdata = await axios.get('http://i1.adis.ws/s/k2skis/k2snowboarding_1819_cinch-ts.json')
      imgdata = imgdata.data
      console.log(imgdata)
    } catch (error) {
      console.error(error);
    }
    return { entry: res, bio: res.bio, imgdata: imgdata }
  },
  methods: {
    time: () => {
      let time = '';
      const d = new Date();
      time += d.getHours()
      time += `:${d.getMinutes()}`
      time += `:${d.getSeconds()}`
      return time
    }
  }
}
</script>

<style scoped>
  img {
    max-height: 200px;
  }
</style>
