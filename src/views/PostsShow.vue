<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    destroyPost: function () {
      if (confirm("Are you sure about that?")) {
        axios.delete(`/posts/${this.post.id}`).then((response) => {
          console.log(response.data);
          this.$router.push("/posts");
        });
      }
    },
  },
};
</script>

<template>
  <div class="posts-show">
    <img v-bind:src="post.image" alt="" />
    <h2>{{ post.title }}</h2>
    <h2>{{ post.body }}</h2>
    <div>
      <button><router-link v-bind:to="`/posts/${post.id}/edit`">Edit</router-link></button>
      |
      <button v-on:click="destroyPost()">Delete</button>
    </div>
  </div>
</template>
