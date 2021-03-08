<template>
  <v-app>
    <v-main>
      <MainPage/>
    </v-main>
    <v-footer
        dark
        padless
    >
      <v-card-text class="py-2 white--text text-center">
        <strong>Шабашев Иван - </strong>
        <a class="white--text" href="https://github.com/shabashev-ivan">https://github.com/shabashev-ivan</a>
      </v-card-text>
    </v-footer>
  </v-app>
</template>

<script>
import MainPage from './components/MainPage';

export default {
  name: 'App',
  components: {
    MainPage,
  },
};
</script>
