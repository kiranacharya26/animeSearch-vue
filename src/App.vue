<template>
  <div class="app">
    <header>
      <h1>My Anime</h1>
      <h3>Search for your favariote anime here</h3>
      <form class="search-box" @submit.prevent="handleSearch">
        <input
          type="search"
          class="search-field"
          placeholder="Search for an anime"
          required
          v-model="search"
        />
      </form>
    </header>
    <main>
      <div class="cards" v-if="animeList.length > 0">
        <Card v-for="anime in animeList" :key="anime.mal_id" :anime="anime" />
      </div>
      <div v-else class="no-results">
        <h2>No results</h2>
      </div>
    </main>
  </div>
</template>

<script>
import { ref } from '@vue/reactivity'
import Card from './components/Card.vue'
export default {
  components: { Card },
  setup() {
    const search = ref('')
    const animeList = ref([])

    const handleSearch = async () => {
      animeList.value = await fetch(
        `https://api.jikan.moe/v3/search/anime?q=${search.value}`
      )
        .then((res) => res.json())
        .then((data) => data.results)
      search.value = ''
    }
    return {
      search,
      animeList,
      handleSearch,
    }
  },
}
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  font-family: Arial, Helvetica, sans-serif;
}
header {
  display: flex;
  align-items: center;
  flex-direction: column;
}
input {
  max-width: 600px;
  width: 30rem;
  height: 2rem;
}
.no-results {
  margin-top: 2rem;
  margin-left: 2rem;
}
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  margin-top: 3rem;
  align-items: center;
}
</style>
