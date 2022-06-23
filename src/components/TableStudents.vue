<template>
  <table class="table-students">
    <tr>
      <td class="sort-number-group" @click="sortNumberGroup">
        <div v-if="revers">группа ▼</div>
        <div v-else>группа ▲</div>
      </td>
      <td class="sort-lastname" @click="sortLastName">
        <div v-if="revers">фамилия ▼</div>
        <div v-else>фамилия ▲</div>
      </td>
      <td>имя</td>
      <td>отчество</td>
      <td>пол</td>
      <td class="sort-date" @click="sortDate">дата рождения</td>
      <td></td>
    </tr>
    <tr
      class="students"
      v-for="(item, index) in PaginateData"
      :key="item.id"
      :class="{ active: selectStudent === item.id - 1 }"
    >
      <td @click="targetStud(item, index)">
        {{ item.numberGroup }}
      </td>
      <td @click="targetStud(item, index)">{{ item.lastname }}</td>
      <td @click="targetStud(item, index)">{{ item.firstName }}</td>
      <td @click="targetStud(item, index)">{{ item.midleName }}</td>
      <td @click="targetStud(item, index)">{{ item.gender }}</td>
      <td @click="targetStud(item, index)">{{ item.date }}</td>
      <td>
        <ButtonDeleteStudent
          :item="item"
          @delStudent="delStudent"
        ></ButtonDeleteStudent>
      </td>
    </tr>
  </table>
</template>

<script>
import ButtonDeleteStudent from "../components/v-button-delete-student.vue";

export default {
  name: "TableStudents",
  data() {
    return {};
  },
  props: {
    students: Array,
    selectStudent: Number,
    PaginateData: Array,
    revers: Boolean,
  },
  methods: {
    delStudent(item) {
      this.$emit("delStudent", item);
    },
    //выделить студента из списка
    targetStud(item, index) {
      this.$emit("targetStud", item, index);
    },
    sortLastName() {
      this.$emit("sortLastName");
    },
    sortNumberGroup() {
      this.$emit("sortNumberGroup");
    },
    reverseString(str) {
      return str.split("").revers().join("");
    },
  },
  components: {
    ButtonDeleteStudent,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.table-students {
  text-align: center;
  border-collapse: collapse;
  font-family: sans-serif;
  height: 100%;
  display: inline-block;
}
td,
tr {
  border: 1px solid rgb(0, 0, 0);
  padding: 5px 10px;
}
.active {
  background-color: rgb(122, 254, 85);
}
.students:hover {
  cursor: pointer;
}
.delete-icon {
  width: 20px;
}
.sort-number-group:hover {
  cursor: row-resize;
  background-color: rgb(230, 230, 230);
}
.sort-lastname:hover {
  cursor: row-resize;
  background-color: rgb(230, 230, 230);
}
</style>