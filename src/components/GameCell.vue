<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "GameCell",
  props: {
    value: {
      type: String as () => "red" | "yellow" | "blue" | null,
      default: null,
    },
  },
});
</script>

<template>
  <div
    class="w-12 h-12 rounded-full border-2 border-blue-700 bg-blue-200 flex items-center justify-center overflow-hidden"
  >
    <transition name="drop" mode="out-in">
      <div
        v-if="value"
        :key="value + Math.random()"
        :class="[
          'w-10 h-10 rounded-full',
          value === 'red'
            ? 'bg-red-500'
            : value === 'yellow'
            ? 'bg-yellow-400'
            : 'bg-blue-500',
        ]"
      />
    </transition>
  </div>
</template>

<style scoped>
.drop-enter-active {
  transition: transform 0.4s ease-out;
}
.drop-enter-from {
  transform: translateY(-100px);
}
.drop-enter-to {
  transform: translateY(0);
}
</style>
