<template>
  <div v-if="posts.length > 0">
    <h3>List of Posts</h3>
    <transition-group name="post-list">
      <post-item
        v-for="post
        in posts"
        :key="post.id"
        :post="post"
        @remove="$emit('remove', post)"
      />
    </transition-group>
  </div>
  <h2
    v-else
    style="color: red"
  >
    List of post is empty
  </h2>
</template>

<script>
import PostItem from "./PostItem.vue";
export default {
  name: "PostList",
  components: {
    PostItem,
  },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
  emits: ["remove"],
};
</script>

<style scoped>
.post-list-item {
  display: inline-block;
  margin-right: 10px;
}
.post-list-enter-active,
.post-list-leave-active {
  transition: all 0.4s ease;
}
.post-list-enter, .post-list-leave-to /* .list-leave-active below version 2.1.8 */ {
  opacity: 0;
  transform: translateX(30px);
}
.post-list-move {
  transition: transform 1s;
}
</style>