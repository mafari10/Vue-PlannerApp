<template>
  <Navbar />
  <router-view />
</template>

<script>
import Navbar from "./components/Navbar.vue";
export default {
  components: {
    Navbar,
  },
};
</script>

<style >
body {
  background: #f2f2f2;
}
#app {
  font-family: Avenir, Arial, Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 30px auto;
  max-width: 600px;
  color: #555;
}
@media screen and (min-width: 1024px) {
  body {
    place-items: center;
  }
}
</style>
