<template>
  <div class="project">
    <div class="actions">
      <h3 class="text-xl font-bold text-red-300" @click="show = !show">
        {{ project.title }}
      </h3>
      <div class="icons">
        <span class="material-icons">edit</span>
        <span class="material-icons">delete</span>
        <span class="material-icons">done</span>
      </div>
    </div>
    <div class="details" v-if="show">
      <p>{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      show: true,
    };
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
  font-size: 14px;
  margin-left: 10px;
  color: #bbb;
  cursor: pointer;
}
</style>