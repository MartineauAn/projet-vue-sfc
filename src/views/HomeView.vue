<template>
  
  <div id="app" class="flex flex-col h-screen" v-cloak>
    <div class="h-12 sticky top-0 z-50 bg-black">
      <div class="flex justify-between ml-10 p-2 items-center h-full">
        <p class="text-2xl text-white">MOST POPULAR TV SHOW LIST</p>
        <input
          type="text"
          v-model="searchQuery"
          placeholder="Rechercher..."
          @input="searchShows"
          class="p-1 rounded-md w-64"
        />
      </div>
    </div>
    <div
      id="contenu"
      class="flex flex-grow p-5 w-full padding overflow-auto"
      @scroll="onScroll"
    >
      <div class="grid grid-cols-5 gap-8 w-full h-1/5">
        <div
          v-for="show in filteredShows"
          v-bind:key="show.id"
          class="w-full h-full shadow-lg hover:shadow-xl"
        >
        <ShowCard :show="show"/>   
        </div>
      </div>
    </div>
  </div>
</template>
		<script>

    import ShowCard from '../components/ShowCard.vue'
export default {
  name: "HomeView",
  data() {
    return {
      baseUrl: "https://www.episodate.com/tv-show/",
      apiURL: "https://www.episodate.com/api/most-popular?page=",
      page: 0,
      shows: [],
      filteredShows: new Array(),
      searchQuery: "",
    };
  },
  components: {
    ShowCard
  },
  created: function () {
    this.fetchTvShows();
    this.fetchTvShows();
  },

  watch: {},
  methods: {
    searchShows: function () {
      this.filteredShows = this.shows.filter((show) => {
        return show.name.toLowerCase().includes(this.searchQuery.toLowerCase());
      });
    },
    fetchTvShows: async function () {
      try {
        this.page++;
        const response = await axios.get(this.apiURL + this.page);
        console.log(response);
        this.shows = this.shows.concat(response.data.tv_shows);
        this.filteredShows = [...this.shows];
      } catch (err) {
        console.warn(err);
      }
    },
    onScroll({ target: { scrollTop, clientHeight, scrollHeight } }) {
      if (scrollTop + clientHeight >= scrollHeight && this.searchQuery == "") {
        this.fetchTvShows();
      }
    },
  },
};
</script>