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
          <a
            class="flex justify-start h-full w-full hover:cursor-pointer"
            target="_blank"
            v-bind:href="baseUrl + show.permalink"
          >
            <div class="h-full w-1/3 flex items-center p-1">
              <img
                v-bind:src="show.image_thumbnail_path"
                class="h-32 w-32 rounded-md"
                v-bind:alt="show.permalink"
              />
            </div>
            <div class="flex flex-col h-full w-2/3 p-1">
              <div class="flex justify-center">
                <p class="text-md font-bold">
                  {{ show.name }}
                </p>
              </div>

              <div class="flex justify-between flex-grow items-end">
                <div
                  v-bind:class="{
                    'text-green-600 border-green-600 hover:bg-green-600':
                      show.status === 'Running',
                    'text-red-600 border-red-600 hover:bg-red-600':
                      show.status === 'Ended',
                  }"
                  class="
                    bg-white
                    border
                    rounded-xl
                    hover:cursor-default hover:text-white
                  "
                >
                  <p class="text-sm p-1">
                    {{ show.status }}
                  </p>
                </div>
                <div class="flex items-center">
                  <p class="italic text-sm">{{ getYear(show.start_date) }}</p>
                  <p v-if="show.end_date != null" class="italic text-sm">
                    - {{ getYear(show.end_date) }}
                  </p>
                </div>
              </div>
            </div>
          </a>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import Navbar from '@/components/Navbar.vue';
export default {
  components: { Navbar },
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

    getYear: function (date) {
      if (date == null) return "";
      return date.slice(0, 4);
    },

    onScroll({ target: { scrollTop, clientHeight, scrollHeight } }) {
      if (scrollTop + clientHeight >= scrollHeight && this.searchQuery == "") {
        this.fetchTvShows();
      }
    },
  },
};
</script>