<template>
  <div class="home">
    <FilterNav @filter="current = $event" :current="current" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
        <SingleProject
          :project="project"
          @delete="handleDelete"
          @completed="toggleCompleted"
        />
      </div>
    </div>
  </div>
</template>

<script >
import axios from "axios";
import SingleProject from "../components/SingleProject.vue";
import FilterNav from "../components/FilterNav.vue";
export default {
  name: "Home",
  components: { SingleProject, FilterNav },
  data() {
    return {
      projects: [],
      current: "all",
    };
  },
  computed: {
    filteredProjects() {
      if (this.current === "completed") {
        return this.projects.filter((project) => project.completed);
      }
      if (this.current === "ongoing") {
        return this.projects.filter((project) => !project.completed);
      }
      return this.projects;
    },
  },
  methods: {
    handleDelete(id) {
      // delete by filtering projects id
      this.projects = this.projects.filter((project) => {
        return project.id !== id;
      });
    },
    // toggleCompleted(id) {
    //   // toggle completed status by returning true or false
    //   let p = this.projects.filter((project) => {
    //     return project.id === id;
    //   });
    //   p[0].completed = !p[0].completed;
    //   console.log(p);
    // },
    // Using find method
    toggleCompleted(id) {
      let p = this.projects.find((project) => {
        return project.id === id;
      });
      if (p) {
        p.completed = !p.completed;
        console.log(p);
      }
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

