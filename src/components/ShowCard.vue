<template>
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
</template>
  
  <script>
  export default {
    name: 'ShowCard',
    props: {
      show: {}
    },
    methods: {
    getYear: function (date) {
      if (date == null) return "";
      return date.slice(0, 4);
    },
  },
  }
  </script>
  
  