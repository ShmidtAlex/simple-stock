<template>
  <div id="app">
    <div class="nav-bar">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>      
    </div>
    <router-view/>    
  </div>
</template>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
}

.nav-bar {
  height: 50px;
  background: linear-gradient(to right, #2C7516, #38B712, #43D218);
  display: flex;
  justify-content: center;
  align-items: center;
  color: white;
  a {
    color: white;
    margin: 0 10px;
  }
  a:hover {
    font-weight: 800;
    color: white;
  }
}
#nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
