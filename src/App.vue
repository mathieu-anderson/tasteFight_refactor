<template>
  <div id="app">
    <h1 class="pointer"
    v-on:click="reload()">tasteFight
    </h1>
      <searchMovie></searchMovie>
  </div>
</template>

<script>
import searchMovie from './components/searchMovie'

export default {
  name: 'app',
  components: {
    searchMovie
  }
}
</script>

<style>

h1 {
  font-size: 40pt;
  font-weight: bold;
text-shadow: 1px 1px 4px rgba(150, 150, 150, 0.98);
cursor: pointer;
}

.big {
  font-size: 14pt;
}

.pointer {
  cursor: pointer;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
