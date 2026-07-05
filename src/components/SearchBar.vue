<template>
<div class="flex justify-center items-center gap-4 my-8">
<input
  v-model="search"
  type="text"
  placeholder="Rechercher une série..."
  class="w-full max-w-lg rounded-lg bg-slate-800 border border-slate-700 px-4 py-3 text-white placeholder-gray-400 focus:ring-2 focus:ring-blue-500"
/>
<button
  class="rounded-lg bg-blue-600 px-6 py-3 font-semibold hover:bg-blue-700 transition mt-6 hover:scale-105" @click="handleSearch"
>Rechercher </button>

</div>

<p class="text-gray-400 text-center mb-8">
  <p v-if="search">
  Vous recherchez : {{ search }}
</p>
  <span class="font-semibold text-white">   
    {{ search }}
  </span>
</p>
</template>  

<script setup >

import { ref } from 'vue'

const search = ref('')
const emit = defineEmits (['search'])

function handleSearch() {
  emit('search', search.value)
}

</script>

<style scoped >
.search-bar {
    display : flex;
    align-items : center;
    justify-content : center;
    margin : 20px 0;
}

.input {
    padding: 20px;
    margin: 10px;
}
</style>
