<script>
export default {
  name: "Footer",
  props: {
    text: String,
  },
};
</script>

<template>
  <footer class="bg-white">
    <div class="container py-6 text-center leading-none">{{ text }}</div>
  </footer>
</template>
