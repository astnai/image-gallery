<template>
  <div class="min-h-screen bg-gray-50 py-10">
    <h1 class="text-4xl font-bold text-center text-gray-800 mb-10">Image Gallery</h1>
    <ImageGallery />
  </div>
</template>

<script>
import ImageGallery from './components/ImageGallery.vue'

export default {
  components: { ImageGallery },
}
</script>
