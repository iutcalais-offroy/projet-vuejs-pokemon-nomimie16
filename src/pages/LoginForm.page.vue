<script setup>
import { ref } from 'vue';
import {NButton, NCard, NText} from 'naive-ui';

const loginEmail = ref('');
const loginPassword = ref('');
const registerEmail = ref('');
const registerPassword = ref('');

const handleLogin = () => {
  // Logique de connexion
  console.log('Connexion avec', loginEmail.value, loginPassword.value);
};

const handleRegister = () => {
  // Logique d'inscription
  console.log('Inscription avec', registerEmail.value, registerPassword.value);
};

const switchToRegister = () => {
  // Logique pour passer à l'onglet d'inscription
  const tabs = document.querySelector('.n-tabs');
  if (tabs) {
    const registerTab = tabs.querySelector('[name="register"]');
    if (registerTab) {
      registerTab.click();
    }
  }
};
</script>



<template>
  <n-card class="login-container">
    <n-tabs type="line">
      <n-tab-pane name="login" tab="Connexion">
        <n-form @submit.prevent="handleLogin">
          <n-form-item label="Email:" path="loginEmail">
            <n-input type="email" placeholder="Entrez votre email" v-model:value="loginEmail" required />
          </n-form-item>
          <n-form-item label="Mot de passe:" path="loginPassword">
            <n-input type="password" placeholder="Entrez votre mot de passe" v-model:value="loginPassword" required />
          </n-form-item>
          <n-button type="primary" native-type="submit">Se connecter</n-button>
          <div class="link-container">
            <n-text>Pas de compte ? <a href="#" @click.prevent="switchToRegister">Inscrivez-vous</a></n-text>
          </div>
        </n-form>
      </n-tab-pane>
      <n-tab-pane name="register" tab="Inscription">
        <n-form @submit.prevent="handleRegister">
          <n-form-item label="Email:" path="registerEmail">
            <n-input type="email" placeholder="Entrez votre email" v-model:value="registerEmail" required />
          </n-form-item>
          <n-form-item label="Mot de passe:" path="registerPassword">
            <n-input type="password" placeholder="Entrez votre mot de passe" v-model:value="registerPassword" required />
          </n-form-item>
          <n-form-item label="Confirmation mot de passe:" path="registerPassword">
            <n-input type="password" placeholder="Entrez votre mot de passe" v-model:value="registerPassword" required />
          </n-form-item>
          <n-button type="primary" native-type="submit">S'inscrire</n-button>
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