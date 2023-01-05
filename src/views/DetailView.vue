<template>
  <div
      class="flex flex-grow p-5 w-full padding overflow-auto"
    >
  <div class="h-full w-full grid grid-cols-2">
    <div class="h-full w-full">
      <img class="object-fit" v-bind:src="detail.image_path" v-bind:alt="detail.permalink">
    </div>
    <div class="h-full w-full">

    </div>
  </div>
  </div>
</template>

<script>

  export default {
    name: "DetailView",
    data(){
      return {
        detail: new Array(),
      };
      
    },
    created: function () {
      this.fetchTvShow();
    },
    methods:{
        fetchTvShow: async function() {
            try {
              const response = await axios.get("https://www.episodate.com/api/show-details?q=" + this.$route.params.title);
              this.detail = this.detail.concat(response.data.tvShow)[0];
              //console.log(this.detail)
            } catch (err) {
              console.warn(err);
            }
        }
    }
  }

</script>