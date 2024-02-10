<script>
export default {
  name: "Footer",
  props: {
    footerText: String,
  },
};
</script>

<template>
  <footer class="bg-white">
    <div class="container py-6 text-center leading-none">{{ footerText }}</div>
  </footer>
</template>
