
<template>
  <div class="bg-slate-800 rounded-xl shadow-lg overflow-hidden hover:scale-105 transition duration-300">

    <img
      v-if="posterPath"
      :src="posterPath"
      :alt="title"
      class="w-full h-80 object-cover"
    />

    <div
      v-else
      class="w-full h-80 flex items-center justify-center bg-slate-700 text-gray-400"
    >
      🎬 Aucune image
    </div>

    <div class="p-5">

      <h2 class="text-xl font-bold text-white">
        {{ title }}
      </h2>

      <p class="mt-2 text-yellow-400">
        ⭐ {{ rating }}
      </p>

      <p class="text-gray-300 mt-1">
        🎭 {{ genre }}
      </p>

      <button
        class="mt-5 w-full bg-blue-600 hover:bg-blue-700 text-white py-2 rounded-lg transition"
      >
        Voir plus
      </button>

    </div>

  </div>
</template>

<script setup>
defineProps ({
    title : String,
    rating : Number,
    posterPath :String,
    genre : String

})
</script>

<style scoped >
.card {
    border: 1px solid #ccc;
    padding: 20px;
    margin: 10px;
    width: 200px;
    }

.card img {
    width: 100%;
    height: auto;
    margin-bottom: 10px;
    }    
</style>
