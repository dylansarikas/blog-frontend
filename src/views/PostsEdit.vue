<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      errors: [],
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    updatePost: function () {
      axios
        .patch(`/posts/${this.post.id}`, this.post)
        .then((response) => {
          console.log("Edit Post:", response.data);
          localStorage.setItem("flashMessage", "Recipe successfully updated!");
          this.$router.push(`/posts/${this.post.id}`);
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <form v-on:submit.prevent="updatePost()">
      <h1>Edit Post</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <p>Current post: {{ post }}</p>
      <div>
        <label>Title:</label>
        <input type="text" v-model="post.title" />
      </div>
      <div>
        <label>Body:</label>
        <input type="text" v-model="post.body" />
      </div>
      <div>
        <label>Image:</label>
        <input type="text" v-model="post.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>
