<template>
  <el-row :gutter="20">
    <el-col class="grid-content pb-4" :span="6" v-for="abc in arr" :key="abc">
      <button
        class="
          min-w-full
          px-4
          py-2
          transition-all
          shadow-base
          border-2 border-gray-200
          rounded-xl
        "
      >
        <div class="flex items-center">
          <el-avatar class="border-2 border-white animate-pulse"></el-avatar>
          <div
            class="ml-2 rounded-md h-4 animate-pulse w-32 min-h-3 bg-gray-200"
          >
            <!-- ({{ person.dob.age }} {{ person.gender[0].toUpperCase() }}) -->
          </div>
        </div>
      </button>
    </el-col></el-row
  >
</template>

<script>
export default {
  name: "PeopleLoader",
  props: {
    noOfPeople: Number,
  },
  data() {
    return {
      arr: [...Array(this.noOfPeople).keys()],
    };
  },
};
</script>

<style lang="scss" scoped>
</style>