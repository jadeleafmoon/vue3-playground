<template>
  <h1>Welcome to the blog!</h1>
  <pre></pre>
  <BlogPost v-for="blogPost in blogPosts" :blogPost="blogPost" />
</template>

<script>
import BlogPost from "./components/BlogPost.vue"

export default {
  name: 'App',
  data() {
    return {
      blogPosts: [
        { title: "Blog Post 1", text: "Some text 1 ..." },
        { title: "Blog Post 2", text: "Some text 2 ..." },
        { title: "Blog Post 3", text: "Some text 3 ..." },
      ]
    }
  },
  components: { BlogPost }
}
</script>

<style>

</style>
