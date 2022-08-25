<template>
  <h1>USER</h1>
  {{ response }}
</template>

<script setup>
const { find } = useStrapi4();

const response = await find("users/me", {
  populate: ["cv", "populate", "cv.job_experience"],
});
</script>
