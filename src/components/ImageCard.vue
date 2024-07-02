<template>
  <div :class="cardClasses">
    <img :src="image.urls.small" :alt="image.alt_description" class="w-full h-full object-cover transition-opacity duration-500" :class="{ 'opacity-0': !loaded, 'opacity-100': loaded }" @load="loaded = true">
    <div class="p-4">
      <p class="text-gray-700 text-sm">{{ image.alt_description }}</p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ImageCard',
  props: ['image'],
  data() {
    return {
      loaded: false,
    }
  },
  computed: {
    cardClasses() {
      const sizeClass = Math.random() > 0.5 ? 'row-span-2' : ''
      return `rounded-lg overflow-hidden shadow-lg bg-white transform transition duration-300 hover:scale-105 ${sizeClass}`
    }
  }
}
</script>
