<template>
  <br />
  <div class="pagination">
    <button @click="prevPage" :disabled="pageNamber < 1">назад</button>
    <input
      class="input-number-students"
      type="number"
      @keydown.enter="changeStudentSize"
      v-model="StudentSize"
    />
    <button @click="nextPage" :disabled="pageNamber === pageCount - 1">
      вперед
    </button>
  </div>
  <br />
</template>

<script>
export default {
  name: "PaginationBox",
  data() {
    return {
      StudentSize: 4,
    };
  },
  props: {
    pageNamber: Number,
    size: Number,
    pageCount: Number,
  },
  methods: {
    prevPage() {
      this.$emit("prevPage");
    },
    nextPage() {
      this.$emit("nextPage");
    },
    changeStudentSize() {
      this.$emit("changeStudentSize", this.StudentSize);
    },
  },
};
</script>

<style scoped>
.input-number-students {
  width: 30px;
}
</style>