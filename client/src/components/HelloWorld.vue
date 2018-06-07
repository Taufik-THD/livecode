<template>
  <div class="hello"  style="height:100%;">

    <div class="row">
      <div class="col s4" style="margin:9% 0 0 35%;">
        <form class="col s12">
          <h4 style="text-align:left"> <b>Sign In</b> </h4>
          <div class="row">
            <div class="input-field col s12" style="padding-right:15px;">
              <input id="email" type="email" class="validate" v-model='email'>
              <label for="email">Email</label>
            </div>
            <div class="input-field col s12" style="padding-right:15px;">
              <input id="name" type="text" v-model='name'>
              <label for="name">Name</label>
            </div>
          </div>
          <a class="btn btn-block" style="width:100%; color:white" @click='login'>Sign In</a>
        </form>
      </div>
    </div>

  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'Homepage',
  created () {
    if (localStorage.hasOwnProperty('authorization')) {
      this.$router.push('/user')
    }
  },
  data () {
    return {
      email: '',
      name: ''
    }
  },
  methods: {
    login () {
      // manual login
      const UserData = {
        email: this.email,
        name: this.name
      }
      axios({
        method: 'post',
        url: 'http://35.197.135.159/request-token',
        data: UserData
      }).then((response) => {
        const token = JSON.stringify(response.data.uuid)
        localStorage.setItem('authorization', token);
        this.$router.push('/user')
        this.email = ''
        this.name = ''
      }).catch((err) => {
        console.log(err)
      })
    }
  }
}

</script>

<style scoped>
ul {
  list-style-type: none;
  padding: 0;
}
a {
  color: #dfe6e9;
}

nav {
  -webkit-transform: none;
  transform: none;
  text-align: left;
  background-color: #2d3436;
  font-family: sans-serif;
  text-align: center;
}
.navmedia{
  padding: 0 5 0 0;
  background-color: transparent;
  border: none;
  margin-bottom: 13%;
}
.socmed{
  height:50px;
  width: 81.5px;
  text-align: center;
  font-size: 50px;
  margin:9% 0 5px 20%;
}
li{
  margin-right:10px;
}
.tooltip {
    position: relative;
    display: inline-block;
    border-bottom: 1px dotted black;
}

.tooltip .tooltiptext {
    visibility: hidden;
    width: 120px;
    background-color: #555;
    color: #fff;
    text-align: center;
    border-radius: 6px;
    padding: 5px 0;
    position: absolute;
    z-index: 1;
    bottom: 125%;
    left: 50%;
    margin-left: -60px;
    opacity: 0;
    transition: opacity 0.3s;
    font-size: 12px;
}

.tooltip .tooltiptext::after {
    content: "";
    position: absolute;
    top: 100%;
    left: 50%;
    margin-left: -5px;
    border-width: 5px;
    border-style: solid;
    border-color: #555 transparent transparent transparent;
}

.tooltip:hover .tooltiptext {
    visibility: visible;
    opacity: 1;
}
</style>
