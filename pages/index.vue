<template>
  <div>
    <div v-html="bio"/>
    <img :src="img"/>
    <div v-html="imgdata"/>
  </div>
</template>

<script>
import Stack from '~/plugins/entry'
import axios from 'axios'

export default {
  data () {
    return {
      bio: '',
      img: 'http://i1.adis.ws/i/k2skis/tubbs_1718_flex-trk-mens_pivot.jpg?h=300&w=400',
      imgdata: ''
    }
  },
  async asyncData() {
    let res = await Stack.getEntry('team_members', 'blt3ec29586cf35b4d6')
    let imgdata;
    try {
      imgdata = await axios.get('http://i1.adis.ws/i/k2skis/tubbs_1718_flex-trk-mens_pivot.json');
      console.log(imgdata.data);
    } catch (error) {
      console.error(error);
    }
    return { entry: res, bio: res.bio, imgdata: imgdata.data }
  }
}
</script>

<style>

</style>
