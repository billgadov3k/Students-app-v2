<template>
  <div class="stud-search">
    <form action="#" class="search" onsubmit="event.preventDefault()">
      <input
        type="text"
        class="form_search__input"
        placeholder="поиск"
        v-model="inputSearch"
        @keypress="filterStuds"
      />
      <!-- <input
        type="text"
        class="input-lastname-search"
        placeholder="фамилия"
        v-model="inputSearchLastname"
      /> -->
      <!-- <input
        type="number"
        class="input-group-search"
        placeholder="группа"
        v-model="inputSearchGroup"
      /> -->
      <!-- <button class="btn-filter">найти студента</button> -->
    </form>
  </div>
</template>

<script>
export default {
  name: "StudSearchBox",
  data() {
    return {
      inputSearch: "",
    };
  },
  props: {
    students: Array,
  },
  methods: {
    //** Фильтруем студентов */
    filterStuds() {
      this.$emit("filterStuds", this.filteredStudentsList);
    },
  },
  computed: {
    filteredStudentsList() {
      return this.students.filter(
        (item) =>
          item.firstName
            .toLowerCase()
            .includes(this.inputSearch.toLowerCase()) ||
          item.midleName
            .toLowerCase()
            .includes(this.inputSearch.toLowerCase()) ||
          item.lastname.toLowerCase().includes(this.inputSearch.toLowerCase())
      );
    },
  },
};
</script>

<style scoped>
* {
  text-align: left;
}

input {
  margin-right: 10px;
}
.stud-search {
  margin-bottom: 10px;
}
</style>