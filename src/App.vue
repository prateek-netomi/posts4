<template>
  <div id="app">
    <h2 class="my-3 font-bold text-xl">Random People</h2>
   <div class="block">
    <span class="demonstration">Slide to fetch more/less data</span>
    <el-slider
    class="mx-16"
      v-model="people"
      :step="10"
      show-stops>
    </el-slider>
  </div>
    <HelloWorld :noOfPeople="people" msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
import HelloWorld from "./components/PeopleView.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
  },
  data() {
  return {
    people: 5,
  }
},
};
</script>

<style>
#app {
  font-family: "Helvetica Neue", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.el-slider__button{
  border: 2px solid rgb(73, 41, 216) !important;
}
.el-slider__bar{
        background-color: rgb(73, 41, 216) !important;

}
</style>
