<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: { title: "", body: "" },
      errors: [],
      sadStatus: "",
    };
  },
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPostParams)
        .then((response) => {
          console.log("New Post:", response.data);
          localStorage.setItem("flashMessage", "Recipe successfully created!");
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.sadStatus = error.response.status;
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

<template>
  <form>
    <h1>Create a New Post</h1>
    <!-- newPostParams : {{ newPostParams }} -->
    <img v-if="sadStatus" v-bind:src="`https://http.cat/${sadStatus}`" alt="" />
    <ul>
      <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
    </ul>
    <div class="form-group">
      <label for="exampleInputTitle1">Title</label>
      <input
        type="text"
        v-model="newPostParams.title"
        class="form-control"
        id="exampleInputTitle1"
        aria-describedby="titleHelp"
        placeholder="Enter Title"
      />
      <small id="titleHelp" class="form-text text-muted">
        {{ 25 - newPostParams.title.length }} characters remaining
      </small>
    </div>
    <div class="form-group">
      <label for="exampleInputBody1">Body</label>
      <input
        type="text"
        class="form-control"
        id="exampleInputBody1"
        placeholder="Enter Body Text"
        v-model="newPostParams.body"
      />
      <small class="danger" v-if="newPostParams.body.length < 8">Must be at least 8 characters long!</small>
      <small class="danger" v-if="newPostParams.body.length > 140">Must be less than 140 characters</small>
    </div>
    <div class="form-group">
      <label for="exampleInputImage1">Image</label>
      <input
        type="text"
        class="form-control"
        id="exampleInputImage1"
        placeholder="Enter Image URL"
        v-model="newPostParams.image"
      />
    </div>
    <div class="form-check">
      <input type="checkbox" class="form-check-input" id="exampleCheck1" />
      <label class="form-check-label" for="exampleCheck1">This checkmark is useless!</label>
    </div>
    <button type="submit" class="btn btn-primary">Submit</button>
  </form>

  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      newPostParams : {{ newPostParams }}
      <h1>New Post</h1>
      <img v-if="sadStatus" v-bind:src="`https://http.cat/${sadStatus}`" alt="" />
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label>Title:</label>
        <input type="text" v-model="newPostParams.title" />
        <br />
        <small>{{ 25 - newPostParams.title.length }} characters remaining</small>
        <br />
      </div>
      <br />
      <div>
        <label>Body:</label>
        <input type="text" v-model="newPostParams.body" />
        <br />
        <small class="danger" v-if="newPostParams.body.length < 8">Must be at least 8 characters long!</small>
        <small class="danger" v-if="newPostParams.body.length > 140">Must be less than 140 characters</small>
      </div>
      <br />
      <div>
        <label>Image:</label>
        <input type="text" v-model="newPostParams.image" />
      </div>
      <input type="submit" value="Submit" />
    </form>
  </div>
</template>

<style scoped>
.danger {
  color: rgb(171, 45, 45);
}
</style>
