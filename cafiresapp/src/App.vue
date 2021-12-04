<template>
  <div id="app">
    <!-- <div id="nav"> -->
      <!-- <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link> | -->
      <!-- <router-link to="/mapbox">Mapbox</router-link> |
      <router-link to="/mapbox2">Mapbox 2</router-link> | -->
      <!-- <router-link to="/d3map">D3 Map</router-link> | -->
      <!-- <router-link to="/d3layout">D3 Layout</router-link> | -->
      <!-- <router-link to="/d3resp">D3 Responsive </router-link> -->
    <!-- </div> -->

    
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background: #121212;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

h1 {
  margin-top: 10%;
}

body {
    background-color: #121212;
}
</style>
