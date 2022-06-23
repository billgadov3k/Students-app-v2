<template>
  <button class="btn-del-student" @click="delStudent(item)">
    <img class="delete-icon" src="../assets/delete-icon.png" alt="" />
  </button>
</template>

<script>
export default {
  name: "ButtonDeleteStudent",
  data() {
    return {};
  },
  props: {
    item: {
      type: Object,
    },
  },
  methods: {
    delStudent(item) {
      this.$emit("delStudent", item);
    },
  },
};
</script>

<style scoped>
.delete-icon {
  width: 20px;
}
</style>