<template>
  <img alt="Vue logo" src="./assets/logo.png">
  <Weather/>
</template>

<script lang="ts">
import { Options, Vue } from 'vue-class-component';
import Weather from './components/Weather.vue';

@Options({
  components: {
    Weather,
  },
})

export default class App extends Vue {
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
