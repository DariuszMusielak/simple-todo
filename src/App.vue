<template>
  <div class="app">
    <!-- <div class="nav">
      <router-link to="/">Todo</router-link> |
    </div> -->
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App',
};
</script>

<style lang="scss">
  @import url('https://fonts.googleapis.com/css?family=Montserrat:300,400,600,800');

  * {
    box-sizing: border-box;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
  }

  .nav {
    background: #455A64;
    padding: 10px;
    color: white;
    * {
      color: white;
    }
  }

  body {
    font-family: Montserrat, sans-serif;
    margin: 0;
    padding: 0;
    background: #CFD8DC;
  }
</style>
