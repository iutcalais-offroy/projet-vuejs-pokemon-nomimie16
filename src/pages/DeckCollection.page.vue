<script lang="ts" setup>
import { ref } from 'vue';
import {NButton, NCard, NText} from 'naive-ui';
import axios from 'axios';

const pokemonList = async () => {
  //connexion
    
  try {
    const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/pokemon-cards/',
    {
      
    });
    console.log('pokemon :', response.data);

  } catch (error) {
    console.error('Erreur lors de l\'inscription:', error);
  }

};

</script>




<template>
  <n-card title="Card with Cover">
    <template #cover>
      <img src="https://07akioni.oss-cn-beijing.aliyuncs.com/07akioni.jpeg">
    </template>
    Card Content
  </n-card>
</template>






<style scoped>
.n-card {
  max-width: 300px;
}
</style>