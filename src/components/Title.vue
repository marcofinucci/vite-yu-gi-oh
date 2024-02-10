<script>
export default {
  name: "Title",
  props: {
    text: String,
  },
};
</script>

<template>
  <div class="text-lg font-medium xl:text-2xl">{{ text }}</div>
</template>
