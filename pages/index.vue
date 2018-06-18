<template>
  <p v-html="bio"/>
</template>

<script>
import fetch from 'isomorphic-fetch'
import contentstack from 'contentstack'

const Stack = contentstack.Stack(process.env.CONTENTSTACK_API, process.env.CONTENTSTACK_TOKEN, 'staging')

export default {
  data () {
    return {
      bio: ''
    }
  },
  created() {
    const self = this
    const Query = Stack.ContentType('team_members').Entry('blt3ec29586cf35b4d6')
    Query.fetch()
    .then(function success(entry) {
      entry = entry.toJSON()
      self.entry = entry
      self.bio = entry.bio
      self.imgs = entry.lifestyle_photos
    }, function error(err) {
      console.log(err)
    });
  },
  mounted() {

  }
}
</script>

<style>

</style>
