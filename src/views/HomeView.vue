<template>
  <main class="min-h-screen bg-gradient-to-br from-slate-950 via-slate-900 to-blue-950 text-white px-8 py-10">
    <div class="max-w-7xl mx-auto">

      <h1 class="text-6xl font-extrabold text-center text-blue-400 tracking-wide">
           🎬 MOVIX
      </h1>

      <p class="text-center text-gray-300 mt-5 mb-12 text-lg">
          Decouvrir vos films et séries préférés.
      </p>
      <SearchBar @search="handleSearch" />

      <h2 class="text-3xl font-bold mt-20 mb-10">

        🔥 Films populaires
      </h2>

<div v-if="loading" class="text-center text-xl text-blue-400 my-8">
  Chargement...
</div>

<div
  v-else-if="movies.length === 0"
  class="text-center text-red-400 text-xl my-8"
>
   Aucun résultat trouvé.
</div>

      <div
      v-else
      class="grid grid-cols-2 md:grid-cols-4 xl:grid-cols-6 gap-8 justify-items-contents">
        <MovieCard
          v-for="movie in movies"
          :key="movie.id"
          :title="movie.title"
          :rating="movie.rating"
          :posterPath="movie.poster"
          :genre="movie.genre"
        />
      </div>

    </div>
  </main>

  <footer class="mt-16 text-center text-gray-500 text-sm">
  © 2026 MOVIX • Développé avec Vue.js & Tailwind CSS Version 1.0
</footer>
</template>

<script setup>
import SearchBar from '@/components/SearchBar.vue'
import MovieCard from '@/components/MovieCard.vue';

import { ref, onMounted } from 'vue'

const movies = ref([])
const loading = ref(false)

async function fetchMovies(query) {
  loading.value = true
  try {
    const response = await fetch(`https://api.tvmaze.com/search/shows?q=${query}`)

    const data = await response.json()

    movies.value = data.map(item => ({
  id: item.show.id,
  title: item.show.name,
  rating: item.show.rating.average ?? "N/A",
  poster: item.show.image?.medium ?? "",
  genre: item.show.genres[0] ?? "Inconnu"
}))

  } catch (error) {
    console.error(error)
  }

  loading.value = false
}

 onMounted(() => {
  fetchMovies('mo')
})

function handleSearch(query) {
  console.log("Recherche reçue :", query)
  fetchMovies(query)
}

///function handleSearch(query) {
  //if (query.trim() === '') {
    //fetchMovies('Batman')
    //return
  //}

  //fetchMovies(query)
//}


</script>

<style scoped>
.home {
  padding : 2rem;
}
.movie-list {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
}
h1 {
  text-align: center;
}

h2 {
  margin: 20px 0;
}

  
</style>