<template>
  <div class="card">
    <a :href="anime.url">
      <img :src="anime.image_url" alt="Anime poster" />
      <h3>{{ anime.title }}</h3>
    </a>
  </div>
</template>

<script>
export default {
  props: ['anime'],
}
</script>
<style lang="scss">
a {
  text-decoration: none;
}
img {
  object-fit: cover;
}
.card {
  text-align: center;
}
</style>
