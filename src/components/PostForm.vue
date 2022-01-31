<template>
  <form @submit.prevent>
    <h4>Create post</h4>
    <my-input
      placeholder="Name"
      v-focus
      v-model="post.title"
    />
    <my-input
      placeholder="Description"
      v-model="post.body"
    />
    <my-button
      @click="createPost"
      style="align-self: flex-end; margin-top: 15px"
    >Create</my-button>
  </form>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
      };
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
}
</style>