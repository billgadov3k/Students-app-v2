<template>
  <div class="form-block">
    <form
      action="#"
      class="add-students-form"
      onsubmit="event.preventDefault()"
    >
      <div class="div-label-form">
        <label class="label-form" for="firstName">Имя</label>
        <input
          id="firstName"
          type="text"
          name="firstName"
          v-model="studData.firstName"
        />
      </div>
      <div class="div-label-form">
        <label class="label-form" for="midleName">Отчество</label>
        <input
          id="midleName"
          type="text"
          name="midleName"
          v-model="studData.midleName"
        />
      </div>
      <div class="div-label-form">
        <label class="label-form" for="lastname">Фамилия</label>
        <input type="text" name="lastname" v-model="studData.lastname" />
      </div>
      <div class="div-label-form">
        <label class="label-form" for="gender">Выберете пол</label>
        <select name="gender" v-model="studData.gender">
          <option disabled selected value>-- выберете пол --</option>
          <option value="мужской">мужской</option>
          <option value="женский">женский</option>
        </select>
      </div>
      <div class="div-label-form">
        <label class="label-form" for="numberGroup">Номер группы</label>
        <select name="numberGroup" v-model="studData.numberGroup">
          <option v-for="item in groupList" :key="item.id">{{ item }}</option>
        </select>
      </div>
      <div class="div-label-form">
        <label class="label-form" for="date">Дата рождения</label>
        <input type="date" name="date" v-model="studData.date" />
      </div>
      <button
        class="btn-add-student"
        v-if="selectStudent === null"
        @click="addStudent"
      >
        добавить студента
      </button>
      <button
        class="btn-add-student"
        v-if="selectStudent !== null"
        @click="editStudent"
      >
        изменить студента
      </button>
    </form>
  </div>
</template>

<script>
export default {
  name: "AddStudentsBox",
  data() {
    return {
      studData: this.studentData,
    };
  },
  props: {
    groupList: Array,
    selectStudent: Number,
    studentData: Object,
  },
  methods: {
    addStudent() {
      this.$emit("addStudent", this.studData);
    },
    editStudent() {
      this.$emit("editStudent", this.studData);
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.form-block {
  border: 1px solid rgb(56, 56, 56);
  padding: 10px;
  text-align: right;
  width: 300px;
  height: 100%;
}
.div-label-form {
  margin-bottom: 5px;
}
.label-form {
  margin-right: 10px;
}
</style>