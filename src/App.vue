<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import MarkImage from './components/MarkImage.vue'

const markers = ref([]);
watchEffect(() => {
  console.log(markers.value)
})
</script>

<template>
  <MarkImage v-model:markers="markers" width="1600" height="1067"
    src="https://upload.wikimedia.org/wikipedia/commons/b/b1/Goat_face.jpg" />
</template>
