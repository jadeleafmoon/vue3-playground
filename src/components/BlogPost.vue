<template>
  <div class="post card">
    <h1> {{ blogPost.title }} </h1>
    <p> {{ blogPost.text }} </p>
    <button @click="handleMarkAsRead">Mark as Read</button>
  </div>
</template>

<script>

export default {
  props: ['blogPost'],
  methods: {
    handleMarkAsRead() {
      this.$emit('handleMarkAsRead');
    }
  }
}

</script>

<style scoped>

.post {
  background-color: lightcoral;
}
</style>