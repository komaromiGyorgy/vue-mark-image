<template>
  <div class="image-marker">
    <slot :onClick="handleImageClick">
      <img class="image-marker__image" :src="src" v-bind="$attrs" @click="handleImageClick" />
    </slot>
    <div v-for="(marker, index) in markers" :key="index" class="image-marker__marker" :class="{
      'image-marker__marker--default': !hasMarkerSlot,
      'image-marker__marker--disable': disable,
    }" :style="getItemPosition(marker)" @click="handleMarkerClick(marker)">
      <slot name="marker" :marker="marker" :index="index">
        <div></div>
      </slot>
    </div>
  </div>
</template>

<script setup lang="ts">
import { computed, useSlots, type PropType } from 'vue'

type Marker = { x: number, y: number }
const props = defineProps({
  markers: {
    type: Array as PropType<Marker[]>,
    default: () => [],
    required: true,
  },
  src: {
    type: String,
    default: ''
  },
  bufferLeft: {
    type: Number,
    default: 12,
  },
  bufferTop: {
    type: Number,
    default: 12,
  },
  alt: {
    type: String,
    default: 'Markers',
  },
  disable: {
    type: Boolean,
    default: false,
  },
});
const slots = useSlots();


const emit = defineEmits<{
  (event: 'update:markers', markers: Marker[]): void
  (event: 'click:marker', marker: Marker): void
}>()

const markerArray = computed({
  get() {
    return props.markers;
  },
  set(value) {
    emit('update:markers', value);
  },
});
const hasMarkerSlot = computed(() => {
  return !!slots?.marker?.();
});

function handleImageClick(event: MouseEvent) {
  if (event && 'target' in event) {
    if (event.target && 'getBoundingClientRect' in event.target && typeof event.target.getBoundingClientRect === 'function') {
      const imagePosition = event.target.getBoundingClientRect();
      const scrollY = window.scrollY;
      const [y, x] = calculateMarkerPosition(
        event,
        imagePosition,
        scrollY,
        props.bufferLeft,
        props.bufferTop
      );
      emit('update:markers', [...markerArray.value, { y, x }]);
    }
  }

}
function handleMarkerClick(marker: Marker) {
  emit('click:marker', marker);
}
function getItemPosition(marker: Marker) {
  return {
    top: `${marker.y}%`,
    left: `${marker.x}%`,
  };
}
function calculateMarkerPosition(
  mousePosition: MouseEvent,
  imagePosition: DOMRect,
  scrollY: number,
  bufferLeft: number,
  bufferTop: number
) {
  const pixelsLeft = mousePosition.clientX - imagePosition.left;
  let pixelsTop;
  if (imagePosition.top < 0) {
    pixelsTop = mousePosition.pageY - scrollY + imagePosition.top * -1;
  } else {
    pixelsTop = mousePosition.pageY - scrollY - imagePosition.top;
  }
  const top = ((pixelsTop - bufferTop) * 100) / imagePosition.height;
  const left = ((pixelsLeft - bufferLeft) * 100) / imagePosition.width;
  return [top, left];
}
</script>
<style scoped>
.image-marker {
  position: relative;
  height: 100%;
  width: 100%;
}

.image-marker__image {
  width: 100%;
  height: 100%;
}

.image-marker__marker {
  position: absolute;
}

.image-marker__marker--disable {
  cursor: not-allowed;
  pointer-events: none;
}

.image-marker__marker--default {
  cursor: pointer;
  width: 25px;
  height: 25px;
  background-color: coral;
  border-radius: 50%;
  color: white;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: all 0.2s ease-in-out;
  animation: append-animate 0.2s ease-in-out;
}

@keyframes append-animate {
  from {
    transform: scale(0);
    opacity: 0;
  }

  to {
    transform: scale(1);
    opacity: 1;
  }
}
</style>
