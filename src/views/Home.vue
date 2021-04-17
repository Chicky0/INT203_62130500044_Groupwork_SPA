<template>
  <div class="home">
  <home :icecreams="icecreams" @add-tofav="addToFav"></home>  
  </div>
</template>


<script>
// @ is an alias to /src
import Home from '../components/MainHome.vue'

export default {
  components: {
    "home": Home
  },
  data(){
    return{
      icecreams:[],
      favList:[]
    };
  },
  methods:{
    async fetchIcecreams(){
      const res = await fetch("http://localhost:5000/icecreams")
      const data = await res.json();
      return data
    },
    async fetchFavIcecreams() {
      const res = await fetch("http://localhost:5000/favList");
      const data = await res.json();
      return data;
    },
    async addToFav(menu) {
      var boolean = true;
      try {
        if (boolean) {
          const res = await fetch("http://localhost:5000/favList", {
            method: "POST",
            headers: {
              "content-type": "application/json",
            },
            body: JSON.stringify({
              name: menu.name,
              description: menu.description,
              id: menu.id,
            }),
          });
          const data = await res.json();
          this.favList = [...this.favList, data];
        } else {
          alert("You already have in FavList");
        }
      } catch (error) {
        console.log(`Could not save! ${error}`);
      }
    },
  },
    async created(){
      this.icecreams =  await this.fetchIcecreams();
    }
  }
</script>
