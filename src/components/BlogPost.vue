<template>
  <div class="post">
    <h1> {{ blogPost.title }} </h1>
    <p> {{ blogPost.text }} </p>
  </div>
</template>

<script>

export default {
  props: ['blogPost'],
}

</script>

<style scoped>

.post {
  background-color: lightcoral;
  margin: 10px;
  padding: 10px;
  border-radius: 10px;
}
</style>