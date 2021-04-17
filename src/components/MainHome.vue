<template>
  <img class="w-72 h-72 pb-4 mx-auto" alt="icecream logo" src="../assets/logo.jpg">
  <div class="bg-white ml-52 mr-52 rounded-lg pl-2">
    <div class="pt-2 text-base">Menu List</div>
    <div v-for="i in icecreams" :key="i.id">{{i.id}}. {{ i.name }} <cbutton v-on:click="addToFav(i)"><slot></slot></cbutton></div> 
  </div>
</template>

<script>
export default {
  props: {
    icecreams: {
      type: Array,
      require: true
    }
  },
  data() {
    return {};
  },
  methods: {
    addToFav(i){
      console.log(i)
      this.$emit("add-tofav",i)
    }
  }
}
</script>