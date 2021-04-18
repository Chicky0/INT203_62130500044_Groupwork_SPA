<template>
  <img class="w-72 h-72 pb-4 mx-auto" alt="icecream logo" src="../assets/logo.jpg">
  <div class="bg-white ml-48 mr-48 rounded-lg pl-2 pb-2">
    <div class="text-center text-xl pt-2">Welcome to Ice-cream Shop...</div>
    <div class="text-base">Menu List...</div>
    <div v-for="i in icecreams" :key="i.id">{{i.id}}. {{ i.name }}
      <br v-if="i.edit">
      <input v-if="i.edit" type="text" v-model="editName" class="bg-red-500"/>
      <cbutton v-if="!i.edit" @click="addToFav(i)"><slot></slot></cbutton>
      <button v-if="!i.edit" @click="editIcecream(i)"><img src="../assets/edit.svg"><slot></slot></button>
      <button v-if="i.edit" @click="confirmName(i)"><img src="../assets/confirm.svg"><slot></slot></button>
      <button v-if="i.edit" @click="cancelEdit(i)"><img src="../assets/cancel.svg"><slot></slot></button>
      </div> 
  </div>
</template>

<script>
export default {
  emits:['add-tofav','confirm-name'],
  props: {
    icecreams: {
      type: Array,
      require: true
    }
  },
  data() {
    return {
      editName: ""
    };
  },
  methods: {
    addToFav(i){
      console.log(i)
      this.$emit("add-tofav",i)
    },
    editIcecream(i){
      // console.log(i)
      i.edit=true
    },
    confirmName(i){
      // console.log(i.id)
      i.edit=false
      console.log(this.editName)
      this.$emit("confirm-name",i,this.editName)
      this.editName = "";
    },
    cancelEdit(i){
      // console.log(i)
      i.edit=false;
    }
  }
}
</script>