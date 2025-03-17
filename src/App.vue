<script lang="ts" setup>
import {NConfigProvider} from 'naive-ui';
import HeaderMenu from './components/HeaderMenu.component.vue';
</script>

<template>
  <n-config-provider>
    <n-layout>
      <n-layout-header class="header">
        <HeaderMenu/>
      </n-layout-header>
      <n-layout-content class="content">
        <n-space justify="center">
          <n-message-provider>
            <RouterView/>
          </n-message-provider>
        </n-space>
      </n-layout-content>
    </n-layout>
  </n-config-provider>
</template>

<style scoped>
.header {
  background-color: rgba(255, 132, 179, 0.203);
}
.content {
  margin-top: 1em;
  margin-left: 3em;
  margin-right: 3em;
}
</style>