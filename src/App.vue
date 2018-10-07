<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
$errorColor: rgb(250, 89, 89);
$shadowColor: #a4a8ac;
$borderColor: #a4a8ac;

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  box-sizing: border-box;
}

.error {
  color: $errorColor;
}

.img-responsive {
  max-width: 100%;
  height: auto;
}
</style>
