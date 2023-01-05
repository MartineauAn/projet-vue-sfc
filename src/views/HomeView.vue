<template>
  
  <div id="app" class="flex flex-col h-screen" v-cloak>
    <Navbar @searchShows="searchShows"/>
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
import Navbar from '../components/Navbar.vue';
import ShowCard from '../components/ShowCard.vue';
export default {
  name: "HomeView",
  data() {
    return {
      baseUrl: "https://www.episodate.com/tv-show/",
      apiURL: "https://www.episodate.com/api/most-popular?page=",
      page: 0,
      shows: [],
      filteredShows: new Array(),
    };
  },
  components: {
    ShowCard,
    Navbar,
  },
  created: function () {
    this.fetchTvShows();
    this.fetchTvShows();
  },

  watch: {},
  methods: {
    searchShows(searchQuery) {
      console.log("zigzig")
      this.filteredShows = this.shows.filter((show) => {
        return show.name.toLowerCase().includes(searchQuery.toLowerCase());
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