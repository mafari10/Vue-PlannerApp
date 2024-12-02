<template>
  <nav class="main_nav">
    <router-link :to="{ name: 'home' }">Projects</router-link>
    <router-link :to="{ name: 'add' }">Add a new Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style scoped>
.main_nav {
  text-align: center;
  margin: 40px auto;
}
.main_nav a {
  display: inline-block;
  text-decoration: none;
  color: #999;
  font-size: 18px;
  margin: 0 10px;
}
a.router-link-active {
  border-bottom: 2px solid #00ce89;
  padding-bottom: 4px;
}
</style>