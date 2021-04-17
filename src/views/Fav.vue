<template>
    <div class="fav">
      <fav :favList="favList" @remove-fromlist="removeIcecreamInFavList"></fav>
    </div>
</template>

<script>
export default {
  name: 'FavList',
  data(){
    return {  
      favList:[],
      linkFavList: "http://localhost:5000/favList",
      have: true
    }
  },
  methods: {
    async fetchFavIcecreams() {
      const res = await fetch("http://localhost:5000/favList");
      const data = await res.json();
      return data;
    },
    async removeIcecreamInFavList(ic) {
      const res = await fetch(`${this.linkFavList}/${ic}`, {
        method: "DELETE",
      });
      res.status === 200
        ? (this.favList = this.favList.filter((i) => i.id !== ic))
        : alert("Error to Delete");
      if (this.favList[0] == undefined) {
        this.have = false;
      }
    }
    },
    async created(){
      this.favList =  await this.fetchFavIcecreams();
  }
}
</script>

