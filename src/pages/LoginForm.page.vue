<script setup>
import { ref } from 'vue';
import {NButton, NCard, NText} from 'naive-ui';
import axios from 'axios';


const loginEmail = ref('');
const loginPassword = ref('');
const registerEmail = ref('');
const registerPassword = ref('');
const verifregisterPassword = ref('');



const switchToRegister = () => {
  //passer onglet d'inscription
  console.log('Passer à l\'onglet d\'inscription');
  const tabs = document.querySelector('.n-tabs');
  if (tabs) {
    const registerTab = tabs.querySelector('[name="register"]');
    if (registerTab) {
      registerTab.click();
    }
  }
};

const switchToConnexion = () => {
  //passer onglet de connexion
  console.log('Passer à l\'onglet de connexion');
  const tabs = document.querySelector('.n-tabs');
  if (tabs) {
    const loginTab = tabs.querySelector('[name="login"]');
    if (loginTab) {
      loginTab.click();
    }
  }
};


const handleLogin = async () => {
  //connexion
    
  try {
    const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/users/login',
    {
      email: loginEmail.value,
      password: loginPassword.value
    });
    console.log('connexion réussi:', response.data);
    localStorage.token = response.data.token;
    localStorage.userid = response.data.user.id;
    // console.log('token:', localStorage.token);
    // console.log('userId:', localStorage.user.id);
    window.location.href = '/deck-builder';
  } catch (error) {
    console.error('Erreur lors de l\'inscription:', error);
  }

};

const handleRegister = async () => {
  //inscription
  console.log('Inscription avec', registerEmail.value, registerPassword.value);
  console.log('Formulaire de connexion soumis');
  if (registerPassword.value !== verifregisterPassword.value) {
    console.error('Les mots de passe ne correspondent pas');
    return;
    
  }
  try {
    const response = await axios.post('https://pokemon-api-seyrinian-production.up.railway.app/users',
    {
      email: registerEmail.value,
      password: registerPassword.value
    });
    console.log('Inscription réussie:', response.data);
    window.location.reload();
  } catch (error) {
    console.error('Erreur lors de l\'inscription:', error);
  }
};

</script>



<template>
  <n-card class="login-container">
    <n-tabs type="line">
      <n-tab-pane name="login" tab="Connexion">
        <n-form @submit.prevent="handleLogin">
          <n-form-item label="Email:" path="loginEmail">
            <n-input id="login-email" type="email" placeholder="Entrez votre email" v-model:value="loginEmail" required />
          </n-form-item>
          <n-form-item label="Mot de passe:" path="loginPassword">
            <n-input id="login-password" type="password" placeholder="Entrez votre mot de passe" v-model:value="loginPassword" required />
          </n-form-item>
          <n-button type="primary" @click="handleLogin">Se connecter</n-button>
          <div class="link-container">
            <n-text>Pas de compte ? <a href="#" @click.prevent="switchToRegister">Inscrivez-vous</a></n-text>
          </div>
        </n-form>
      </n-tab-pane>
      <n-tab-pane name="register" tab="Inscription">
        <n-form @submit.prevent="handleRegister">
          <n-form-item label="Email:" >
            <n-input id="register-email" type="email" placeholder="Entrez votre email" v-model:value="registerEmail" required />
          </n-form-item>
          <n-form-item label="Mot de passe:">
            <n-input id="register-password" type="password" placeholder="Entrez votre mot de passe" v-model:value="registerPassword" required />
          </n-form-item>
          <n-form-item label="Confirmation mot de passe:" path="verifregisterPassword">
            <n-input id="register-password-confirm" type="password" placeholder="Entrez votre mot de passe" v-model:value="verifregisterPassword" required />
          </n-form-item>
          <n-button type="primary" @click="handleRegister">S'inscrire</n-button>
          <div class="link-container">
            <n-text>Déjà un compte ? <a href="#" @click.prevent="switchToConnexion">Connectez-vous</a></n-text>
          </div>
        </n-form>
      </n-tab-pane>
    </n-tabs>
  </n-card>
</template>



<style scoped>

</style>