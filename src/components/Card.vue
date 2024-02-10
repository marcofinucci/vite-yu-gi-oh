<script>
export default {
  name: "Card",
  props: {
    card: Object,
  },
};
</script>

<template>
  <div class="aspect-[309/451] w-full bg-gray-200">
    <img class="object-cover" :src="card.card_images[0].image_url" :alt="card.name" />
  </div>
  <div class="mt-4 text-xs font-medium uppercase tracking-wide text-red-700">{{ card.archetype ? card.archetype + " -" : "" }} {{ card.type }}</div>
  <div class="mt-1 font-medium xl:text-lg">{{ card.name }}</div>
</template>
