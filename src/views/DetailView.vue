<template>
  <div>
    <Navbar @searchShows="searchShows" />
    <main class="flex-grow p-5">
      <div class="w-full rounded overflow-hidden shadow-lg">
        <!-- Afficher le titre de la série -->
        <h1 class="font-bold text-3xl mb-2">{{ detail.name }}</h1>
        <!-- Afficher l'image de la série -->
        <div class="flex justify-bewteen">
          <div class="flex justify-center w-1/3">
            <img
              v-bind:src="detail.image_path"
              v-bind:alt="detail.name"
              class=""
            />
          </div>
          <div class="flex justify-center w-2/3 p-2">
            <div class="mt-5">
              <h2 class="text-lg font-bold border-b border-gray-600">
                Summary
              </h2>
              <p class="text-xl mt-2" v-html="detail.description"></p>
            </div>
          </div>
        </div>
        <div class="flex justify-end p-2">
          <div class="mt-2 mr-2">
            <span class="font-bold">Début :</span> {{ detail.start_date }}
            <span v-if="detail.end_date" class="font-bold ml-4">Fin :</span>
            {{ detail.end_date }}
          </div>
          <div
            v-bind:class="{
              'bg-green-500 text-white rounded-full p-1':
                detail.status === 'Running',
              'bg-red-500 text-white rounded-full p-1':
                detail.status === 'Ended',
            }"
            class="w-64"
          >
            {{ detail.status }}
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import Navbar from "../components/Navbar.vue";
export default {
  components: {
    Navbar,
  },
  name: "DetailView",
  data() {
    return {
      detail: new Array(),
    };
  },
  created: function () {
    this.fetchTvShow();
  },
  methods: {
    fetchTvShow: async function () {
      try {
        const response = await axios.get(
          "https://www.episodate.com/api/show-details?q=" +
            this.$route.params.title
        );
        this.detail = this.detail.concat(response.data.tvShow)[0];
        //console.log(this.detail)
      } catch (err) {
        console.warn(err);
      }
    },
  },
};
</script>