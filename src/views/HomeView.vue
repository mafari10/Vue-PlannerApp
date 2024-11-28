<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @completed="toggleDeleted"
        />
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
  methods: {
    handleDelete(id) {
      // delete by filtering projects id
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    toggleDeleted(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      p.completed = !p.completed;
    },
  },
  async mounted() {
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

