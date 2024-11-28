<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject :project="project" />
      </div>
    </div>
  </div>
</template>

<script >
import axios from "axios";
import SingleProject from "../components/SingleProject.vue";
export default {
  name: "Home",
  components: { SingleProject },
  data() {
    return {
      projects: [],
    };
  },
  async created() {
    try {
      const response = await axios.get("http://localhost:3000/projects");
      this.projects = response.data;
      console.log(this.projects);
    } catch (e) {
      console.error("Error getting", e);
    }
  },
};
</script>
<style scoped>
</style>

