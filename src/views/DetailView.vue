<template>
  <div>

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
              this.detail = this.detail.concat(response.data.tvShow);
            } catch (err) {
              console.warn(err);
            }
        }
    }
  }

</script>