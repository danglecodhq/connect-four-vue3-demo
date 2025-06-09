<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "GameCell",
  props: {
    value: {
      type: String as () => "red" | "yellow" | null,
      default: null,
    },
  },
});
</script>

<template>
  <div
    class="w-12 h-12 rounded-full border-2 border-blue-700 flex items-center justify-center bg-blue-200"
  >
    <div
      v-if="value"
      :class="[
        'w-10 h-10 rounded-full',
        value === 'red' ? 'bg-red-500' : 'bg-yellow-400',
      ]"
    />
  </div>
</template>
