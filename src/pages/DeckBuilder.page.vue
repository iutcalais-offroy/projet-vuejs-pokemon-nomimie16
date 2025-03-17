<script lang="ts" setup>
import { ref, onMounted } from 'vue';
import { NButton, NCard, NText } from 'naive-ui';
import axios from 'axios';

const pokeid = ref('12');
const pokemon = ref({
  id: '',
  name: '',
  pokedexId: '',
  typeId: '',
  lifePoints: '',
  imageUrl: '',
  height: '',
  weight: '',
  attackId: '',
  weaknessId: ''
});

const fetchPokemon = async () => {
  try {
    const response = await axios.get(`https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards/${pokeid.value}`);
    console.log('pokemon :', response.data);
    pokemon.value = response.data;
  } catch (error) {
    console.error('Erreur lors de la récupération des informations du Pokémon:', error);
  }
};

onMounted(() => {
  fetchPokemon();
});
</script>

<template>
  <n-card >
    <template #cover>
      <img :src="pokemon.imageUrl" >
    </template>
    <div>
      <p><strong>{{ pokemon.name }}</strong>  {{ pokemon.lifePoints }}</p>
      <p><strong>Type ID:</strong> {{ pokemon.typeId }}</p>
      <p><strong>Life Points:</strong> {{ pokemon.lifePoints }}</p>
      <p><strong>Height:</strong> {{ pokemon.height }} m</p>
      <p><strong>Weight:</strong> {{ pokemon.weight }} kg</p>
      <p><strong>Attack ID:</strong> {{ pokemon.attackId }}</p>
      <p><strong>Weakness ID:</strong> {{ pokemon.weaknessId }}</p>
    </div>
  </n-card>
</template>

<style scoped>
.n-card {
  max-width: 300px;
}
</style>