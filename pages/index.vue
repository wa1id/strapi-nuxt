<template>
  <h1 class="text-3xl font-bold">Strapi Nuxt</h1>
  {{ response }}
</template>

<script setup>
const { find } = useStrapi4();

const response = await find("users", { populate: "*" });
</script>
