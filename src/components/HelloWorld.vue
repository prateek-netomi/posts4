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
      <el-col :span="12"> {{ filtered_people.length }} Results </el-col></el-row
    >
    <el-row :gutter="20">
      <el-col
        class="grid-content pb-4"
        :span="8"
        v-for="(person, index) in filtered_people"
        :key="index"
      >
        <Dialog :person="person" />
      </el-col>
    </el-row>
  </div>
</template>

<script>
import axios from "axios";
import Dialog from "./Dialog.vue";
export default {
  components: { Dialog },
  name: "HelloWorld",
  props: {
    msg: String,
  },
  data() {
    return {
      people: [],
      filtered_people: [],
      info: 0,
      input: "",
    };
  },
  mounted() {
    axios
      .get("https://randomuser.me/api/?results=50&nat=us")
      .then((response) => {
        this.people = response.data.results;
        this.filtered_people = response.data.results;
      });
  },
  methods: {
    filter() {
      this.filtered_people = this.people.filter((person) =>
        JSON.stringify(person)
          .replaceAll("{", " ")
          .replaceAll("}", " ")
          .includes(this.input)
      );
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.main-card:hover {
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.12), 0 0 6px rgba(0, 0, 0, 0.04);
}
.thumbnail {
  width: 40px;
  height: 40px;
  border-radius: 4px;
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
.flex {
  display: flex;
}
.ai-center {
  align-items: center;
}
.m-l-2 {
  margin-left: 1rem;
}
.bg-blue {
  background: blue;
}
.bg-pink {
  background: pink;
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
