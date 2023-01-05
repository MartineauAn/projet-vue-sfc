<template>
    <div class="h-12 sticky top-0 z-50 bg-black">
      <div class="flex justify-between ml-10 p-2 items-center h-full">
        <p class="text-2xl text-white">MOST POPULAR TV SHOW LIST</p>
        <input
          type="text"
          v-model="searchQuery"
          placeholder="Rechercher..."
          @input="updateSearch"
          class="p-1 rounded-md w-64"
        />
      </div>
    </div>
</template>
<script>
export default {
  name: 'Navbar',
  data(){
    return{
        searchQuery: ''
    }
  },
  methods:{
    updateSearch(){
        this.$emit('searchShows', this.searchQuery)
        console.log("zig")
    },
  }
};
</script>
