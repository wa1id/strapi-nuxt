<script setup>
definePageMeta({  middleware: 'auth'})

const { find } = useStrapi4();

const response = await find("cvs", { populate: "*" });

const user = useStrapiUser()
console.log(user)
</script>

<template>
  <div class="page">
    <div v-if="response" class="page__head">
      <div class="image-wrapper object-fit">
        <img :src="`http://localhost:1337${response.data[0].attributes.profile_image.data.attributes.url}`" alt="">
      </div>
      <h1>
        {{response.data[0].attributes.first_name}}
        {{response.data[0].attributes.last_name}}
      </h1>
      <p>{{response.data[0].attributes.profession}}</p>
    </div>
    <div class="page__content">
        <div class="contact">
            <h2>Contact</h2>
            <div class="contact__options">
                <div class="address">
                <p>{{response.data[0].attributes.address.street_and_number}}</p>
                <p>
                    {{response.data[0].attributes.address.zipcode}}
                    {{response.data[0].attributes.address.city}}      
                </p>
                <p>{{response.data[0].attributes.address.country}}</p>
                </div>
                <div class="ways">
                    <p>Phone: {{response.data[0].attributes.phone}}</p>
                    <p>email: {{response.data[0].attributes.email}}</p>
                </div>
            </div>
        </div>
      <div class="bio">
        <h2>Bio</h2>
        <p>{{response.data[0].attributes.bio}}</p>
      </div>
      <div class="job-experience">
        <h2>Job Experience</h2>
        <div class="list">
            <div v-for="{id, title, description} in response.data[0].attributes.job_experience" :key="id">
                <h3>{{ title }}</h3>
                <p>{{ description }}</p>
            </div>
        </div>
      </div>
      <div class="education">
        <h2>Education</h2>
        <div class="list">
            <div v-for="{id, title, description} in response.data[0].attributes.education" :key="id">
                <h3>{{ title }}</h3>
                <p>{{ description }}</p>
            </div>
        </div>
      </div>
      <div class="awards">
        <h2>Awards</h2>
        <div class="list">
            <div v-for="{id, title, description} in response.data[0].attributes.awards" :key="id">
                <h3>{{ title }}</h3>
                <p>{{ description }}</p>
            </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Poppins:ital,wght@0,300;0,400;0,500;0,700;0,900;1,600&display=swap');

* {
    font-family: 'Poppins', sans-serif;
}

.object-fit img {
  @apply w-full h-full object-cover;
  object-position: 50% 50%;
}

.page {
  @apply min-h-screen bg-[#042940] flex flex-col gap-12 py-16;
}

.page__head {
  @apply flex flex-col items-center;
}

.image-wrapper {
  @apply w-60 h-60 rounded-full overflow-hidden;
}

h1 {
  @apply text-[#DBF227] font-black text-3xl pt-4 pb-2;
}

h2 {
  @apply text-[#DBF227] font-bold text-2xl pb-2;
}

h3 {
  @apply text-[#9FC131] font-medium text-xl pb-2;
}

p {
  @apply text-white;
}

.page__content {
  @apply max-w-5xl px-4 mx-auto;
}

.page__content {
  @apply flex flex-col gap-10;
}

.contact__options {
    @apply grid grid-cols-2 gap-x-12;
}

.list {
    @apply flex flex-col gap-6;
}
</style>

