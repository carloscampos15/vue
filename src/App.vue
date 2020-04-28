<template>
  <v-app id="app">
    <Container></Container>
  </v-app>
</template>

<script>
import Container from "./components/Container.vue";

import Vue from 'vue'
import { rtdbPlugin } from 'vuefire'

Vue.use(rtdbPlugin)

export default {
  name: "App",
  components: {
    Container
  }
};
</script>

<style>
</style>
