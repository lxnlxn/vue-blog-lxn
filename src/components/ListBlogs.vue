<template>
  <div v-theme:column="'wide'" id="show-blogs">
    <h1>测试Minxin混入</h1>
    <input type="text" v-model="search" placeholder="search something.... " />
    <div v-for="(blog,index) in filterdBlogs" :key="index" class="single-blog">
      <h2 v-rainbow>{{blog.title | to-uppercase}}</h2>
      <article>{{blog.body | snippet}}</article>
    </div>
  </div>
</template>

<script>
import searchMixin from "../mixins/searchMixins";
export default {
  name: "ListBlogs",
  data() {
    return {
      blogs: [],
      search: ""
    };
  },
  created() {
    this.$axios.get("/posts").then(res => {
      console.log(res.data);
      this.blogs = res.data.slice(0, 10);
    });
  },

  directives: {
    rainbow: {
      bind(el, binding, vnode) {
        el.style.color =
          "#" +
          Math.random()
            .toString(16)
            .slice(2, 8);
      }
    }
  },
  filters: {
    // "to-uppercase": function(value) {
    //   return value.toUpperCase();
    // }
    toUppercase(value) {
      return value.toUpperCase();
    }
  },
  mixins: [searchMixin]
};
</script>

<style scoped>
#show-blogs {
  max-width: 800px;
  margin: 0 auto;
}
.single-blog {
  padding: 20px;
  margin: 20px 0;
  box-sizing: border-box;
  background: limegreen;
}

input[type="text"] {
  padding: 8px;
  width: 100%;
  box-sizing: border-box;
}
</style>
