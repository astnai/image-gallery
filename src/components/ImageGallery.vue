<template>
  <div class="max-w-5xl mx-auto px-4">
    <div class="relative mb-4">
      <input
        v-model="query"
        @input="debouncedFetchImages"
        placeholder="Search..."
        class="p-3 border rounded-lg w-full shadow-md focus:outline-none focus:ring-2 focus:ring-indigo-500"
      >
      <svg class="w-6 h-6 absolute top-3 right-3 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-4.35-4.35m1.35-5.65a7.5 7.5 0 11-15 0 7.5 7.5 0 0115 0z"></path>
      </svg>
    </div>
    <div v-if="error" class="text-red-500 text-center mb-4">{{ error }}</div>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-6">
      <ImageCard v-for="image in images" :key="image.id" :image="image" />
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import ImageCard from './ImageCard.vue'
import debounce from 'lodash/debounce'

export default {
  name: 'ImageGallery',
  components: { ImageCard },
  data() {
    return {
      images: [],
      query: '',
      error: null,
    }
  },
  mounted() {
    this.fetchImages()
  },
  methods: {
    async fetchImages() {
      this.error = null
      try {
        const response = await axios.get(`https://api.unsplash.com/search/photos`, {
          params: {
            query: this.query || 'random',
            client_id: process.env.VUE_APP_UNSPLASH_ACCESS_KEY,
          }
        })
        this.images = response.data.results
      } catch (err) {
        this.error = 'Failed to fetch images. Please try again later.'
        console.error(err)
      }
    },
    debouncedFetchImages: debounce(function() {
      this.fetchImages()
    }, 500),
  }
}
</script>
