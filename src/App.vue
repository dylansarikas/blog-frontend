<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
      flashMessage: null,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
      this.flashMessage = localStorage.flashMessage;
      localStorage.removeItem("flashMessage");
    },
  },
  methods: {},
};
</script>

<!-- <template>
  <div id="nav">
    <router-link to="/">Home</router-link>
    |
    <router-link v-if="!isLoggedIn" to="/signup">Signup</router-link>
    |
    <router-link v-if="!isLoggedIn" to="/login">Login</router-link>
    |
    <router-link v-if="isLoggedIn" to="/logout">Logout</router-link>
    |
    <router-link to="/posts">Post Index</router-link>
    |
    <router-link v-if="isLoggedIn" to="/posts/new">New Post</router-link>
  </div>
  <div v-if="flashMessage">
    {{ flashMessage }}
    <button v-on:click="flashMessage = ''">Dismiss</button>
  </div>
  <router-view />
</template> -->

<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <router-link class="navbar-brand" to="/">Navbar</router-link>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarNavAltMarkup"
        aria-controls="navbarNavAltMarkup"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
        <div class="navbar-nav">
          <router-link class="nav-link active" aria-current="page" to="/">Home</router-link>
          <router-link v-if="!isLoggedIn" class="nav-link" to="/signup">Signup</router-link>
          <router-link v-if="!isLoggedIn" class="nav-link" to="/login">Login</router-link>
          <router-link v-if="isLoggedIn" class="nav-link" to="/logout">Logout</router-link>
          <router-link class="nav-link" to="/posts">Post Index</router-link>
          <router-link v-if="isLoggedIn" class="nav-link" to="/posts/new">New Post</router-link>
          <router-link class="nav-link" to="/bootstrap-posts">Bootstrap Posts</router-link>
        </div>
      </div>
      <form class="form-inline">
        <div class="input-group">
          <div class="input-group-prepend">
            <span class="input-group-text" id="basic-addon1">#</span>
          </div>
          <input
            type="text"
            v-model="titleFilter"
            list="postTitles"
            placeholder="Blog Title"
            aria-label="Username"
            aria-describedby="basic-addon1"
          />
        </div>
      </form>
    </div>
  </nav>
  <div class="container">
    <router-view />
  </div>
</template>
