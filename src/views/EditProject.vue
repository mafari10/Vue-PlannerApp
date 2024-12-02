<template>
  <div>
    <form @submit.prevent="handleUpdate">
      <label for="title">Title</label>
      <input type="text" id="title" v-model="title" required />
      <label for="details">Details</label>
      <textarea type="text" id="details" v-model="details" required />
      <button type="submit">Update Project</button>
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      url: "http://localhost:3000/projects/" + this.id,
    };
  },

  async mounted() {
    try {
      const response = await axios.get(this.url);
      this.title = response.data.title;
      this.details = response.data.details;
    } catch (e) {
      console.error(e.message);
    }
  },
  methods: {
    async handleUpdate() {
      try {
        const response = await axios.patch(this.url, {
          title: this.title,
          details: this.details,
        });
        this.$router.push("/");
      } catch (e) {
        console.error(e.message);
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