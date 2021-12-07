<template>
  <div>
    <el-button
      class="min-w-full hover:bg-purple-100 hover:border-purple-800"
      @click="dialogVisible = true"
    >
      <div class="flex ai-center">
        <el-avatar :src="person.picture.thumbnail"></el-avatar>
        <h3>
          <strong class="m-l-2">
            {{ person.name.first }} {{ person.name.middle }}
            {{ person.name.last }}
          </strong>
          <!-- ({{ person.dob.age }} {{ person.gender[0].toUpperCase() }}) -->
        </h3>
      </div>
    </el-button>

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