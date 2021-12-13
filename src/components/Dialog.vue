<template>
  <div>
    <button
      class="
        min-w-full
        px-4
        py-2 focus:bg-purple-500 focus:text-white
        transition-all shadow-base hover:shadow-lg
        hover:bg-purple-200 hover:border-purple-800
        border-2 border-gray-200
        rounded-xl
      "
      @click="dialogVisible = true"
    >
      <div class="flex items-center">
        <el-avatar class="border-2 border-white" :src="person.picture.thumbnail"></el-avatar>
        <h3 class="ml-2 color-white">
          <strong>
            {{ person.name.first }} {{ person.name.middle }}
            {{ person.name.last }}
          </strong>
          <!-- ({{ person.dob.age }} {{ person.gender[0].toUpperCase() }}) -->
        </h3>
      </div>
    </button>

    <el-dialog
      class="hover:rounded-xl"
      :title="fullName"
      :visible.sync="dialogVisible"
      width="50%"
      :before-close="handleClose"
    >
      <span>
        <div
          class="
            border-2
            rounded-lg
            transition-4 transition
            duration-500
            flex
            hover:border-indigo-400
          "
          :body-style="{ padding: '0px' }"
        >
          <img
            :src="person.picture.large"
            class="rounded-xl m-3 shadow-md border-gray-300 border-4"
          />
          <div style="padding: 14px">
            <p class="font-medium text-left">{{ fullName }}</p>
            <p class="font-medium text-left">{{ person.email }}</p>
            <div class="bottom clearfix">
              <time class="time">{{ person.dob.date }}</time>
            </div>
          </div>
        </div>
      </span>
      <span slot="footer" class="dialog-footer">
        <el-button type="success" class="button">Operating</el-button>
        <el-button type="secondary" @click="dialogVisible = false"
          >Close</el-button
        >
      </span>
    </el-dialog>
  </div>
</template>

<script>
export default {
  props: {
    person: {
      type: Object,
    },
  },
  data() {
    return {
      dialogVisible: false,
    };
  },
  methods: {
    handleClose() {
      return (this.dialogVisible = false);
    },
  },
  computed: {
    fullName() {
      return this.person.name.first + " " + this.person.name.last;
    },
  },
};
</script>

<style  scoped>
.thumbnail {
  width: 40px;
  height: 40px;
  border-radius: 4px;
}
</style>