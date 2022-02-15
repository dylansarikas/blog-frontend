<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log(response.data);
      this.posts = response.data;
    });
  },
  methods: {},
};
</script>

<template>
  <div class="posts-index">
    <h1>Posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>{{ post.title }}</h2>
      <router-link v-bind:to="`/posts/${post.id}`">
        <img v-bind:src="post.image" alt="" />
      </router-link>
    </div>
  </div>
</template>
