<template>
  <div>
    <router-link :to="{ name: 'testpage' }">test</router-link>
    <div v-html="bio"/>
    <img src="http://i1.adis.ws/i/k2skis/tubbs_1718_flex-trk-mens_pivot.jpg?h=300&w=400"/>
    <div v-html="imgdata"/>
  </div>
</template>

<script>
import Stack from '~/plugins/entry'
import axios from 'axios'

export default {
  async asyncData() {
    let res = await Stack.getEntry('team_members', 'blt3ec29586cf35b4d6')
    let imgdata
    try {
      imgdata = await axios.get('http://i1.adis.ws/i/k2skis/tubbs_1718_flex-trk-mens_pivot.json')
      imgdata = imgdata.data
    } catch (error) {
      console.error(error);
    }
    return { entry: res, bio: res.bio, imgdata: imgdata }
  }
}
</script>

<style>

</style>
