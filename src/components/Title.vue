<script>
export default {
  name: "Title",
  props: {
    title: String,
  },
};
</script>

<template>
  <div class="text-lg font-medium xl:text-2xl">{{ title }}</div>
</template>
