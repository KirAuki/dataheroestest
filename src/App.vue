<template>
  <div id="app">
    <h1>Rick and Morty Characters</h1>
    <div class="filters">
      <input v-model="filters.name" type="text" placeholder="Name" />
      <select v-model="filters.status">
        <option value="">Status</option>
        <option value="Alive">Alive</option>
        <option value="Dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button @click="applyFilters">Apply</button>
    </div>
    <Pagination :info="info" :currentPage="currentPage" @page-change="fetchCharacters" />
    <div class="characters">
      <CharacterCard v-for="character in characters" :key="character.id" :character="character" />
    </div>
    <Pagination :info="info" :currentPage="currentPage" @page-change="fetchCharacters" />
  </div>
</template>

<script>
import { ref, reactive, onMounted } from 'vue';
import axios from 'axios';
import CharacterCard from './components/CharacterCard.vue';
import Pagination from './components/Pagination.vue';

export default {
  name: 'App',
  components: {
    CharacterCard,
    Pagination,
  },
  setup() {
    const characters = ref([]);
    const info = ref({});
    const currentPage = ref(1);
    const filters = reactive({
      name: '',
      status: '',
    });

    const fetchCharacters = async (page = 1) => {
      currentPage.value = page;
      const { data } = await axios.get('https://rickandmortyapi.com/api/character', {
        params: {
          page,
          name: filters.name,
          status: filters.status,
        },
      });
      characters.value = data.results;
      info.value = data.info;
    };

    const applyFilters = () => {
      fetchCharacters(1);
    };

    onMounted(() => {
      fetchCharacters();
    });

    return {
      characters,
      info,
      currentPage,
      filters,
      fetchCharacters,
      applyFilters,
    };
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  margin: 0 auto;
  display: block;
}

.filters {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
}

.filters input,
.filters select {
  margin-right: 10px;
  padding: 5px;
}

.characters {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  justify-content: center;
}

button {
  padding: 5px 10px;
}
</style>
