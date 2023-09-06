<template>
  <h1>Welcome to the blog!</h1>

  <h2>Counter + $emit</h2>
  <p>Number of times blog posts were read: {{ blogsRead }}</p>

  <h2>$refs</h2>
  <p ref="myRef">Change this text with $refs</p>

  <h2>Computed Properties</h2>
  <p>Enter a number in each field.</p>
  <input v-model="num1" type="number"/>
  <input v-model="num2" type="number"/>
  <p>Sum: {{ sum }}</p>
  <p>Product: {{ product }}</p>

  <h2>Blog Posts</h2>
  <BlogPost 
    v-for="blogPost in blogPosts" 
    :blogPost="blogPost" 
    @handle-mark-as-read="addOne"
  />
</template>

<script>
import BlogPost from "./components/BlogPost.vue"

export default {
  name: 'App',
  components: { BlogPost },
  data() {
    return {
      num1: 0,
      num2: 0,
      blogsRead: 0,
      blogPosts: [
        { title: "Blog Post 1", text: "Some text 1 ..." },
        { title: "Blog Post 2", text: "Some text 2 ..." },
        { title: "Blog Post 3", text: "Some text 3 ..." },
      ]
    }
  },
  computed: {
    sum() {
      return this.num1 + this.num2
    },
    product() {
      return this.num1 * this.num2
    }
  },
  methods: {
    addOne() {
      this.blogsRead += 1
    }
  },
  mounted() {
    this.$refs.myRef.textContent = "New text!"
  }

}
</script>

<style>

</style>
