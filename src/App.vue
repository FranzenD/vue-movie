<template>
  <div id="app">
    <nav id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </nav>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 10px;
  box-sizing: border-box;
}

#nav{
  margin-bottom: 20px;
}

.error {
  color: $errorColor;
}

.img-responsive {
  max-width: 100%;
  height: auto;
}

.trailer {
  margin-bottom: 20px;
  &--small {
    margin-bottom: 10px;
  }
}
.leader {
  margin-top: 20px;
  &--small {
    margin-top: 10px;
  }
}
</style>
