<template>
  <h1>Welcome to the blog!</h1>

  <div class="experiment">
    <h2>Computed Properties</h2>
    <p>Enter a number in each field.</p>
    <input v-model="num1" type="number"/>
    <br>
    <input v-model="num2" type="number"/>
    <p>Sum: {{ sum }}</p>
    <p>Product: {{ product }}</p>
  </div>

  <div class="experiment">
    <h2>$refs</h2>
    <p ref="myRef">Old text.</p>
    <p>Click the following to change the text using $refs:</p>
    <button @click="toggleText">Toggle the Text</button>
  </div>

  <div class="experiment">
    <h2>Counter + $emit</h2>
    <p>Number of times blog posts were read: <strong>{{ blogsRead }}</strong></p>
  </div>

  <div>
    <h2>Blog Posts</h2>
    <BlogPost 
      v-for="blogPost in blogPosts" 
      :blogPost="blogPost" 
      @handle-mark-as-read="addOne"
    />
  </div>

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
    },
    toggleText() {
      const currentText = this.$refs.myRef.textContent;
      if (currentText === "Old text.") {
        this.$refs.myRef.textContent = "New text!"
      } else if (currentText === "New text!") {
        this.$refs.myRef.textContent = "Old text."
      }
    }
  },

}
</script>

<style>

button {
  border-radius: 5px;
  padding: 10px 10px;
  border: 1px solid white;
}

button:hover {
  cursor: pointer;
  background-color: lightcyan;
}

.experiment {
  background-color: lightgray;
  margin: 10px;
  padding: 10px;
  border-radius: 10px;
  max-width: 60%;
}


</style>
