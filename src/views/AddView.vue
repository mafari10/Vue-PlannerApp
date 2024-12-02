<template>
  <div class="form_container">
    <form @submit.prevent="handleSubmit">
      <label for="title">Title</label>
      <input type="text" id="title" v-model="title" required />
      <label for="details">Details</label>
      <textarea type="text" id="details" v-model="details" required />
      <button type="submit">Add Project</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      title: "",
      details: "",
      url: "http://localhost:3000/projects",
    };
  },
  methods: {
    async handleSubmit() {
      let project = {
        title: this.title,
        details: this.details,
        completed: false,
      };
      try {
        // Posted Data to DB using axios
        const response = await axios.post(this.url, project);
        // Redirect to homepage if successful
        this.$router.push("/");
      } catch (e) {
        console.error("Error posting project", e.message);
      }
    },
  },
};
</script>

<style  scoped>
form {
  padding: 20px;
  border-radius: 10px;
  background: #fff;
}
label {
  display: block;
  color: #bbb;
  text-transform: uppercase;
  font-size: 14px;
  font-weight: bold;
  letter-spacing: 1px;
  margin: 20px 0 10px 0;
}
input {
  padding: 10px;
  border: 0;
  border-bottom: 1px solid #ddd;
  border-radius: 3px;
  width: 100%;
  box-sizing: border-box;
}
textarea {
  resize: none;
  width: 100%;
  height: 80px;
  border: 1px solid #ddd;
  border-radius: 3px;
  margin-bottom: 10px;
  box-sizing: border-box;
}
form button {
  display: block;
  padding: 10px;
  background: #00ce89;
  color: white;
  border: 0;
  width: 100%;
  border-radius: 3px;
  font-size: 16px;
  margin: 20px auto 0;
  transition: all 50ms ease-in-out;
}
form button:hover {
  background: #67c9a8;
}
</style>