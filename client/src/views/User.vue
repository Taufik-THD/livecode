<template>
  <div class="home">
    <Header/>
    <Userpage/>
  </div>
</template>

<script>
// @ is an alias to /src
import Userpage from '@/components/Userpage.vue'
import Header from '@/components/Header.vue'

export default {
  name: 'user',
  components: {
    Userpage,
    Header
  }
}
</script>
