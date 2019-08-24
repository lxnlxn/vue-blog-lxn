<template>
  <div class="SingleBlog">
    <button @click="$router.go(-1)">返回</button>
    <h1>{{blog.title}}</h1>
    <article>{{blog.body}}</article>
    <p>{{blog.id}}</p>
    <p>{{blog.userId}}</p>
  </div>
</template>

<script>
export default {
  name: "SingleBlog",
  data() {
    return {
      id: this.$route.params.id,
      blog: {}
    };
  },
  created() {
    // console.log(this.$router.params.id);
    // this.$axios.get("/posts/" + this.id}).then(res => {
    this.$axios.get(`/posts/${this.id}`).then(res => {
      console.log(res.data);
      this.blog = res.data;
    });
  }
};
</script>

<style scoped>
</style>
