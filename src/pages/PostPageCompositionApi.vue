<template>
  <div>
    <h1>Page with posts</h1>
    <my-input
      v-model="searchQuery"
      v-focus
      placeholder="Search...."
    />
    <div class="app__btns">
      <my-button>Create post
      </my-button>
      <my-select
        v-model="selectedSort"
        :options="sortOptions"
      />
    </div>
    <my-dialog v-model:show="dialogVisible">
    </my-dialog>
    <post-list
      :posts="sortedAndSearchedPosts"
      v-if="!isPostsLoading"
    />
    <div v-else>Is loading...</div>

  </div>
</template>

<script>
import PostList from "@/components/PostList";
import MyButton from "@/components/UI/MyButton";
import { usePosts } from "@/hooks/usePosts";
import useSortedPosts from "@/hooks/useSortedPosts";
import useSortedAndSearchedPosts from "@/hooks/useSortedAndSearchedPosts";
export default {
  components: {
    PostList,
    MyButton,
  },
  data() {
    return {
      dialogVisible: false,
      sortOptions: [
        { value: "title", name: "search by name" },
        { value: "body", name: "search by description" },
      ],
    };
  },
  setup() {
    const { posts, totalPages, isPostsLoading } = usePosts(10);
    const { selectedSort, sortedPosts } = useSortedPosts(posts);
    const { searchQuery, sortedAndSearchedPosts } =
      useSortedAndSearchedPosts(sortedPosts);
    return {
      posts,
      totalPages,
      isPostsLoading,
      selectedSort,
      sortedPosts,
      searchQuery,
      sortedAndSearchedPosts,
    };
  },
};
</script>

<style>
h4 {
  margin-bottom: 15px;
}
h1 {
  margin-bottom: 15px;
}

.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
.page__wrapper {
  display: flex;
  margin-top: 15px;
}
.page {
  border: 1px solid black;
  padding: 10px;
}
.current-page {
  border: 2px solid teal;
}
.observer {
  height: 30px;
  background: green;
}
</style>