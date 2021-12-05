<template>
  <div class="">
    <title>{{ msg }}</title>
    <el-row class="mb-4 center">
      <el-col :span="12">
        <el-input
          @change="filter()"
          id="search-input"
          prefix-icon="el-icon-search"
          placeholder="search"
          v-model="input"
          clearable
        >
        </el-input> </el-col></el-row
    ><el-row class="mb-4 center">
      <el-col :span="12"> {{ filtered_posts.length }} Results </el-col></el-row
    >
    <el-row :gutter="20">
      <el-col
        class="grid-content pb-4"
        :span="8"
        v-for="(post, index) in filtered_posts"
        :key="index"
      >
        <el-card class="main-card">
          <h3>
            <strong> {{ post.title }} </strong>
          </h3>
          <p>{{ post.body }}</p>
        </el-card>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      posts: [],
      filtered_posts: [],
      info: 0,
      input: "",
    };
  },
  mounted() {
    axios.get("https://jsonplaceholder.typicode.com/posts").then((response) => {
      this.posts = response.data;
      this.filtered_posts = response.data;
    });
  },
  methods: {
    filter() {
      this.filtered_posts = this.posts.filter((post) =>
        JSON.stringify(post)
          .replaceAll("{", " ")
          .replaceAll("}", " ")
          .includes(this.input)
      );
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.main-card:hover {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}
.main-card {
  height: 15rem;
  transition: all 0.3;
  border-radius: 8px;
}
.pb-4 {
  padding-bottom: 1rem;
}
.mb-4 {
  margin-bottom: 1rem;
}
.box {
  /* height: 15rem; */
  /* margin: 0.4rem; */
  padding: 0.4rem;
  border-radius: 8px;
  box-shadow: 1px 4px 6px rgb(0 0 0 / 20%);
  border: 1px solid rgba(0, 0, 0, 0.3);
  background: aliceblue;
}
p {
  text-align: center;
}
.center {
  width: 100%;
  display: flex;
  align-content: center;
  justify-content: center;
}
/* h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
} */
</style>
