<template lang="html">
  <div class="">
    <div class="row">
      <div class="col s12 m3" v-for='data in pictures'>
        <div class="card teal darken-4">
          <div class="card-image">
            <img :src="data.url" style="height:200px">
          </div>
          <div class="card-content">
            <h5 style="color: white"></h5>
            <p style="color: white"></p>
            <h4 style="color:red;"></h4>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  created () {
    if (!localStorage.hasOwnProperty('authorization')) {
      this.$router.push('/')
    } else {
      this.getImages()
    }
  },
  data () {
    return {
      pictures: null
    }
  },
  methods: {
    getImages () {

      const token = localStorage.getItem('authorization')

      axios({
        method: 'get',
        url: 'http://35.197.135.159/image',
        data: {},
        headers: {
          authorization: token
        }
      }).then((response) => {
        this.pictures = response.data
      }).catch(err => {
        console.log(err);
      })
    }
  }
}
</script>

<style lang="css">
</style>
