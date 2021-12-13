<template>
  <div class="mx-2">
    <title>{{ msg ? msg : "People" }}</title>
    <el-row class="mb-4 flex items-center min-w-full">
      <el-col class="px-2" :span="8">
        <el-switch
          v-model="genderFilter"
          active-text="Male"
          inactive-text="Female"
        >
        </el-switch>
      </el-col>
      <el-col class="px-72" :span="16">
        <input
          class="
            block
            w-full
            border border-gray-300
            rounded-md
            py-2
            pl-2
            pr-3
            shadow-sm
            focus:outline-none
            focus:border-purple-800
            focus:ring-purple-200
            focus:ring-2
            sm:text-sm
          "
          @change="filter()"
          id="search-input"
          prefix-icon="el-icon-search"
          placeholder="search"
          v-model="input"
          clearable
        /> </el-col
    ></el-row>
    <template v-if="loading">
      <PeopleLoader :noOfPeople="noOfPeople" />
    </template>
    <template v-else>
      <!-- <el-row class="mb-4 place-content-center">
        <el-col :span="12">
          {{ loading ? "Loading..." : filtered_people.length + " Results" }}
        </el-col></el-row
      > -->
      <el-row :gutter="20">
        <el-col
          class="grid-content pb-4"
          :span="6"
          v-for="(person, index) in filtered_people"
          :key="index"
        >
          <Dialog :person="person" />
        </el-col>
      </el-row>
    </template>
  </div>
</template>

<script>
import axios from "axios";
import Dialog from "./Dialog.vue";
import PeopleLoader from "./PeopleLoader.vue";
export default {
  components: { Dialog, PeopleLoader },
  name: "HelloWorld",
  props: {
    msg: String,
    noOfPeople: Number,
  },
  data() {
    return {
      people: [],
      filtered_people: [],
      info: 0,
      input: "",
      loading: false,
      genderFilter: false,
    };
  },
  mounted() {
    this.loading = true;
    axios
      .get(`https://randomuser.me/api/?results=${this.noOfPeople}&nat=us`)
      .then((response) => {
        this.people = response.data.results;
        this.filtered_people = response.data.results;
      })
      .finally(() => (this.loading = false));
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
  watch: {
    noOfPeople: {
      handler(newValue) {
        this.loading = true;
        axios
          .get(`https://randomuser.me/api/?results=${newValue}&nat=us`)
          .then((response) => {
            this.people = response.data.results;
            this.filtered_people = response.data.results;
          })
          .catch(() => (this.people = []))
          .finally(() => (this.loading = false));
      },
    },
    genderFilter(val) {
      console.log(val);
    },
  },
};
</script>
<style>
.el-switch__label.is-active {
  color: rgb(73, 41, 216) !important;
}
.el-switch__core {
  background: rgb(73, 41, 216) !important;
}
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
  padding: 0.4rem;
  border-radius: 8px;
  box-shadow: 1px 4px 6px rgb(0 0 0 / 20%);
  border: 1px solid rgba(0, 0, 0, 0.3);
  background: aliceblue;
}
p {
  text-align: center;
}
</style>
