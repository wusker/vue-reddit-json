<template>
  <div id="app">
    <header>
      <h1>r/rarepuppers</h1>
    </header>
    <Posts />
  </div>
</template>

<script>
import Posts from "./components/Posts.vue";

export default {
  name: "App",
  components: {
    Posts
  }
};
</script>

<style>
body {
  margin: 0 auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  background: #2c3e50;
  overflow-x: hidden;
  max-width: 2000px;
}
h1 {
  margin: 0;
  font-size: 1rem;
}
#app {
  color: white;
}
header {
  padding-left: 1vw;
  width: 100%;
  background: black;
  color: white;
}
</style>
