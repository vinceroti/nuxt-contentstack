<template>
  <div>
    <p v-html="bio"/>
    <img :src="img"/>
  </div>
</template>

<script>
import Stack from '~/plugins/entry'

export default {
  data () {
    return {
      bio: '',
      img: 'http://i1.adis.ws/i/k2skis/tubbs_1718_flex-trk-mens_pivot.jpg?h=300&w=400'
    }
  },
  async asyncData() {
    let res = await Stack.getEntry('team_members', 'blt3ec29586cf35b4d6')
    return { entry: res, bio: res.bio }
  }
}
</script>

<style>

</style>
