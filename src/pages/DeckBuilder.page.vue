<script lang="ts" setup>
import { ref, onMounted,computed } from 'vue';
import { NButton, NCard, NText } from 'naive-ui';
import axios from 'axios';

const searchQuery = ref('');

interface Pokemon {
  id: string;
  name: string;
  pokedexId: string;
  type: {
    id: string;
    name: string;
  };
  lifePoints: string;
  imageUrl: string;
  height: string;
  attack: {
    id: string;
    name: string;
    damages: string;
  };
  weight: string;
  attackId: string;
  weaknessId: string;
}


const pokemons = ref<Pokemon[]>([]);


const fetchPokemon = async () => {
  try {
    const response = await axios.get(`https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards/`);
    console.log('pokemon :', response.data);
    pokemons.value = response.data;
  } catch (error) {
    console.error('Erreur lors de la récupération des informations du Pokémon:', error);
  }
};

const filteredPokemons = computed(() => {
  return pokemons.value.filter(pokemon =>
    pokemon.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});


onMounted(() => {
  fetchPokemon();
});
</script>

<template>
  <div id="all">
    <n-input class="search" v-model:value="searchQuery" placeholder="Rechercher un Pokémon par son nom" />
  </div>
    <div class="contenair">
      <n-card  v-for="pokemon in filteredPokemons" :key="pokemon.id" class="n-card">

        <template #cover>
          <img :src="pokemon.imageUrl" >
        </template>
        <div>
          <div class="n-card-title">
            <p><strong>{{ pokemon.name }}</strong></p>
            <img class="type" :src="'https://veekun.com/dex/media/types/en/'+ pokemon.type.name.toLowerCase() +'.png'">

          </div>
          <p><strong class="pv"> PV {{ pokemon.lifePoints }}</strong></p>
          
          <p class="height">Poids : {{ pokemon.height }} | Poid: {{ pokemon.weight }} kg</p>
          <div class="n-card-attack">
            <p><strong>{{ pokemon.attack.name }}</strong></p>
            <p id="damages">{{ pokemon.attack.damages }}</p>
            

          </div>
          <n-button text class="card-button"><img  id="pokeball" :src="'https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/items/poke-ball.png'" ></n-button>
        </div>
      </n-card>
  </div>
</template>

<style scoped>
*{
  font-family: Helvetica, sans-serif;
}

.search{
  min-width: 600px;
  width: 40%;
  /* margin: 2%;
  margin-left: 5%; */
  border-radius: 10px;
}

#all{
  min-width: 600px;
  width: 100%;
  display: flex;    
  justify-content: center;
  margin: 2%;  
}

.n-card {
  max-width: 200px;
  background-color: rgb(244, 243, 243);
  border-radius: 15px;
  border: solid 1px rgb(255, 132, 179);
  box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2);
  transition: transform 0.3s ease-in-out, box-shadow 0.3s ease-in-out;
}

.n-card:hover {
  transform: scale(1.1) rotate(3deg);
  box-shadow: 0 8px 16px rgba(0, 0, 0, 0.3);
  background-color: rgb(226, 226, 226);
  transition: all 0.3s ease-in-out;
}

.contenair {
  display: flex;
  flex-wrap: wrap;
  gap: 20px;
  justify-content: center;
}

.n-card-title {
  display: flex;
  flex-wrap: wrap;
}

.n-card-attack {
  display: flex;
  flex-wrap: wrap;
  background-color: rgba(255, 132, 179, 0.203);
}

#damages{
  margin-left: 50%
}
.type {
  width: 40px;
  height: 20px;
  margin: auto;
}

.pv {
  color: red;
  margin: 0%;
}

p {
  margin: 3%;
  padding: 0%;
}

.height {
  color: gray;
  font-size: 10px;
  text-align: center;
}

#pokeball {
  width: 50px;
  height: 50px;
}
.card-button {
  position: absolute;
  bottom: 150px;
  left: 50%;
  transform: translateX(-50%);
  display: none;
  border: none;
  transition: opacity 0.3s ease-in-out, transform 0.3s ease-in-out;
}

.n-card:hover .card-button {
  display: block;
}

</style>
