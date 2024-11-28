<template>
  <div class="project" :class="{ completed: project.completed }">
    <div class="actions">
      <h3 class="text-xl font-bold text-red-300" @click="show = !show">
        {{ project.title }}
      </h3>
      <div class="icons">
        <span class="material-icons">edit</span>
        <span class="material-icons" @click="deleteItem">delete</span>
        <span
          class="material-icons"
          @click="completed"
          :class="{ tick: project.completed }"
          >done</span
        >
      </div>
    </div>
    <div class="details" v-if="show">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["project"],
  data() {
    return {
      show: true,
      url: "http://localhost:3000/projects/" + this.project.id,
    };
  },
  methods: {
    async deleteItem() {
      try {
        await axios.delete(this.url);
        // emit the deleted id to HomeView
        this.$emit("delete", this.project.id);
      } catch (e) {
        console.error("Error deleting project", e);
      }
    },
    async completed() {
      try {
        await axios.patch(this.url, { completed: !this.project.completed });
        this.$emit("completed", this.project.id);
      } catch (e) {
        console.error("Error completing project", e);
      }
    },
  },
};
</script>

<style scoped>
.project {
  margin: 20px auto;
  background: white;
  padding: 20px 10px;
  border-radius: 9px;
  box-shadow: 1px 2px 3px rgba(0, 0, 0, 0.5);
  border-left: 6px solid rgb(182, 115, 126);
}
h3 {
  cursor: pointer;
}
.actions {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.material-icons {
  font-size: 18px;

  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
.material-icons:hover {
  color: #777;
}
.completed {
  border-left: 6px solid #00ce89;
}
.tick {
  color: #00ce89;
}
</style>