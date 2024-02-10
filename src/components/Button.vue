<script>
export default {
  name: "Button",
  props: {
    text: String,
  },
  emits: ["click-button"],
};
</script>

<template>
  <button class="mx-auto mt-8 table bg-black px-6 py-3 text-white transition-colors hover:bg-gray-800" @click="$emit('click-button')">{{ text }}</button>
</template>
