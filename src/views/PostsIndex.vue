<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: [],
      titleFilter: "",
    };
  },
  created: function () {
    axios.get("/posts").then((response) => {
      console.log(response.data);
      this.posts = response.data;
    });
  },
  methods: {},
  computed: {
    filteredPosts: function () {
      return this.posts.filter((post) => {
        return post.title.toLowerCase().includes(this.titleFilter.toLowerCase());
      });
    },
  },
};
</script>

<template>
  <div class="input-group">
    <div class="form-outline">
      <input type="search" id="form1" class="form-control" />
      <label class="form-label" for="form1">Search</label>
    </div>
    <button type="button" class="btn btn-primary">
      <i class="fas fa-search"></i>
    </button>
  </div>
  <div class="row row-cols-2 row-cols-md-4 g-4">
    <div class="col" v-for="post in filteredPosts" v-bind:key="post.id">
      <div class="card">
        <router-link v-bind:to="`/posts/${post.id}`">
          <img v-bind:src="post.image" class="card-img-top" alt="I'm too lazy to add images in the backend" />
        </router-link>
        <div class="card-body">
          <h5 class="card-title">{{ post.title }}</h5>
          <p class="card-text">
            {{ post.body }}
          </p>
        </div>
      </div>
    </div>
  </div>

  <div class="posts-index">
    <h1>Posts</h1>
    <p>
      Search:
      <input type="text" v-model="titleFilter" list="postTitles" />
    </p>
    <datalist id="postTitles">
      <option v-for="post in posts" v-bind:key="post.id">
        {{ post.title }}
      </option>
    </datalist>
    <transition-group
      appear
      enter-active-class="animate__animated animate__fadeIn"
      leave-active-class="animate__animated animate__fadeOut"
    >
      <div v-for="post in filteredPosts" v-bind:key="post.id">
        <h2>{{ post.title }}</h2>
        <router-link v-bind:to="`/posts/${post.id}`">
          <img v-bind:src="post.image" alt="" />
        </router-link>
      </div>
    </transition-group>
  </div>
</template>
