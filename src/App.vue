<template>
  <h1>Welcome to the blog!</h1>

  <div class="experiment card">
    <h2>Sum and Product</h2>
    <p>Enter a number in each field.</p>
    <input v-model="num1" type="number"/>
    <br>
    <input v-model="num2" type="number"/>
    <p>Sum: {{ sum }}</p>
    <p>Product: {{ product }}</p>
    <p>📖 Learned: computed properties</p>
  </div>

  <div class="experiment card">
    <h2>Change text with refs</h2>
    <p ref="myRef">Old text.</p>
    <button @click="toggleText">Toggle the Text</button>
    <p>📖 Learned: The use of $refs. In this case, the text is changed. </p>
    <p>Careful: refs are used only in special cases.</p>
    <p>Refs are available only after a component is mounted.</p>
  </div>

  <div>

    <h2>Blog Posts</h2>

    <div class="experiment card">
      <h2>Number of times blogs were read:</h2>
      <h3>{{ blogsRead }}</h3>
      <p>📖 Learned: creating a counter button with $emit.</p>
    </div>

    

    <div class="experiment card flex-container">
      <h2>Add a new blog post</h2>
      <input 
        v-model="newBlogTitle" 
        placeholder="Title ..." 
        class="blog-title-input"
      />
      <textarea 
        v-model="newBlogText" 
        placeholder="Write your text here ..."
      />
      <br>
      <button @click="submitBlogPost">Submit</button>
    </div>

    <BlogPost 
      v-for="blogPost in blogPosts" 
      :key="blogPost.id"
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
      newBlogTitle: "",
      newBlogText: "",
      blogsRead: 0,
      blogPosts: [
        { title: "Blog Post 1", text: "Some text 1 ...", id: 1 },
        { title: "Blog Post 2", text: "Some text 2 ...", id: 2 },
        { title: "Blog Post 3", text: "Some text 3 ...", id: 3 },
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
    },
    submitBlogPost() {
      const newId = this.blogPosts[this.blogPosts.length - 1].id + 1;
      const newBlogPost = { 
        title: this.newBlogTitle, 
        text: this.newBlogText,
        id: newId,
      }
      console.log(newBlogPost)
      this.blogPosts.push(newBlogPost)
      this.newBlogTitle = ""
      this.newBlogText = ""
    }
  },

}
</script>

<style>

body {
  font-family: 'Lato', sans-serif;
  background: #eee;

}

#app {
  
  margin: 20px;
  
}

button {
  border-radius: 5px;
  padding: 10px 10px;
  border: 1px solid white;
}

button:hover {
  cursor: pointer;
  background-color: lightcyan;
}

.card {
  margin-top: 10px;
  padding: 10px;
  border-radius: 10px;
  max-width: 60%;

  box-shadow: rgba(0, 0, 0, 0.12) 0px 1px 3px, rgba(0, 0, 0, 0.24) 0px 1px 2px;
}

textarea {
  width: 70%;
  padding: 10px;
  margin-top: 10px;
}

input {
  padding: 10px;
}

.blog-title-input {
  width: 70%;
}

.experiment {
  background-color: white;

}

.flex-container {
  display: flex;
  flex-flow: column;
  align-content: flex-start;
}



</style>
