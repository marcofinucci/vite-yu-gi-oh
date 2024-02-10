<script>
export default {
  name: "Header",
  props: {
    appName: String,
  },
};
</script>

<template>
  <header class="bg-white">
    <div class="container py-4 text-lg font-medium leading-none xl:py-6 xl:text-3xl">{{ appName }}</div>
  </header>
</template>
