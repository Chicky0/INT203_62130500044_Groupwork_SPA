<template>
  <div class="home">
    <center><img class="w-72 h-72" alt="icecream logo" src="../assets/logo.jpg"></center>
    <Helloworld msg="Hi"/>
  </div>
  <div>Hi</div>
</template>

<script>
// @ is an alias to /src
import Helloworld from '@/components/Helloworld.vue'

export default {
  name: 'Home',
  components: {
    Helloworld
  }
}
</script>
