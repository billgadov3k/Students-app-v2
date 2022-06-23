<template>
  <div class="main">
    <h1>Список студентов</h1>
    <stud-search-box :students="students" @filterStuds="filterStuds">
    </stud-search-box>
    <table-students
      @delStudent="delStudent"
      @targetStud="targetStud"
      @sortLastName="sortLastName"
      @sortNumberGroup="sortNumberGroup"
      :students="students"
      :selectStudent="selectStudent"
      :PaginateData="PaginateData"
      :revers="revers"
    ></table-students>
  </div>

  <pagination-box
    @prevPage="prevPage"
    @nextPage="nextPage"
    @changeStudentSize="changeStudentSize"
    :pageNamber="pageNamber"
    :size="size"
    :pageCount="pageCount"
  ></pagination-box>

  <div class="section">
    <add-students-box
      @addStudent="addStudent"
      @editStudent="editStudent"
      :groupList="groupList"
      :selectStudent="selectStudent"
      :studentData="studData"
    ></add-students-box>

    <group-box
      @editGroupNumber="editGroupNumber"
      @targetGroup="targetGroup"
      @addGroupNumber="addGroupNumber"
      @deleteGroup="deleteGroup"
      :groupList="groupList"
      :targetGr="targetGr"
      :targetGruopValue="targetGruopValue"
      :studData="studData"
    ></group-box>
  </div>
</template>

<script>
import TableStudents from "./components/TableStudents.vue";
import AddStudentsBox from "./components/AddStudentsBox.vue";
import StudSearchBox from "./components/StudSearchBox.vue";
import GroupBox from "./components/GroupBox.vue";
import PaginationBox from "./components/PaginationBox.vue";

export default {
  name: "App",
  data() {
    return {
      students: [
        {
          firstName: "Александр",
          midleName: "Петрович",
          lastname: "Чукоткин",
          numberGroup: "222",
          gender: "мужской",
          date: "2005-02-10",
          status: false,
          filter: true,
          id: 1,
        },
        {
          firstName: "Василий",
          midleName: "Геннадьевич",
          lastname: "Иванов",
          numberGroup: "111",
          gender: "мужской",
          date: "2001-05-10",
          status: false,
          filter: true,
          id: 2,
        },
        {
          firstName: "Оксана",
          midleName: "Викторовна",
          lastname: "Синицина",
          numberGroup: "333",
          gender: "женский",
          date: "1995-06-21",
          status: false,
          filter: true,
          id: 3,
        },
        {
          firstName: "Никита",
          midleName: "Сергеевич",
          lastname: "Минин",
          numberGroup: "5555",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 4,
        },
        {
          firstName: "Никита",
          midleName: "Иванович",
          lastname: "Михайлов",
          numberGroup: "444",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 5,
        },
        {
          firstName: "Михаил",
          midleName: "Андреевич",
          lastname: "Киров",
          numberGroup: "111",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 6,
        },
        {
          firstName: "Наталия",
          midleName: "Александровна",
          lastname: "Соколова",
          numberGroup: "111",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 7,
        },
        {
          firstName: "Катерина",
          midleName: "Сергеевна",
          lastname: "Вознесенская",
          numberGroup: "777",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 8,
        },
        {
          firstName: "Александр",
          midleName: "Сергеевич",
          lastname: "Пушкин",
          numberGroup: "555",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 9,
        },
        {
          firstName: "Антон",
          midleName: "Павлович",
          lastname: "Чехонтэ",
          numberGroup: "222",
          gender: "мужской",
          date: "2020-06-10",
          status: false,
          filter: true,
          id: 10,
        },
        {
          firstName: "Оксана",
          midleName: "Владимировна",
          lastname: "Синицина",
          numberGroup: "333",
          gender: "женский",
          date: "1995-06-21",
          status: false,
          filter: true,
          id: 11,
        },
        {
          firstName: "Надежда",
          midleName: "Андреевна",
          lastname: "Самолетова",
          numberGroup: "333",
          gender: "женский",
          date: "1995-06-21",
          status: false,
          filter: true,
          id: 12,
        },
      ],
      studData: {
        firstName: "",
        midleName: "",
        lastname: "",
        numberGroup: "",
        gender: "",
        date: "2004-01-01",
        status: true,
        filter: true,
        index: null,
        id: null,
      },
      groupList: [111],
      targetGr: null,
      targetGruopValue: null,
      selectStudent: null,
      pageNamber: 0,
      size: 4,
      id: 12,
      revers: true,
      FilterStudents: [],
    };
  },
  methods: {
    //** СТУДЕНТЫ*/
    // удаляет студента
    delStudent(item) {
      const index = this.students.findIndex((n) => n.id === item.id);
      if (index !== -1) {
        this.students.splice(index, 1);
      }
    },
    // добавить студента
    addStudent(event) {
      if (
        event.firstName == "" ||
        event.midleName == "" ||
        event.lastname == "" ||
        event.numberGroup == "" ||
        event.gender == "" ||
        event.date == ""
      ) {
        console.log("не все поля заполнены");
      } else {
        this.students.unshift({
          firstName: event.firstName,
          midleName: event.midleName,
          lastname: event.lastname,
          numberGroup: event.numberGroup,
          gender: event.gender,
          date: event.date,
          filter: true,
          status: true,
          id: (this.id = this.id + 1),
        });
      }
      this.clear();
    },
    //** Выделяет студента */
    targetStud(item) {
      if (this.selectStudent !== item.id - 1) {
        this.selectStudent = item.id - 1;
        this.studData.firstName = item.firstName;
        this.studData.midleName = item.midleName;
        this.studData.lastname = item.lastname;
        this.studData.gender = item.gender;
        this.studData.numberGroup = item.numberGroup;
        this.studData.date = item.date;
        this.studData.id = item.id;
      } else {
        this.selectStudent = null;
        this.clear();
      }
    },
    //** Редактировать студента */
    editStudent(student) {
      this.students[this.selectStudent] = {
        firstName: student.firstName,
        midleName: student.midleName,
        lastname: student.lastname,
        numberGroup: student.numberGroup,
        gender: student.gender,
        date: student.date,
        filter: true,
        status: true,
        id: this.studData.id,
      };
      this.clear();
      this.selectStudent = null;
    },
    //** очистить поля ввода студента */
    clear() {
      this.studData.firstName = "";
      this.studData.midleName = "";
      this.studData.lastname = "";
      this.studData.numberGroup = "";
      this.studData.gender = "";
      this.studData.date = "2004-01-01";
    },

    //** !!! ГРУППЫ !!!

    //** выберает номер группы из списка
    targetGroup(item, index) {
      if (this.targetGr !== index) {
        this.targetGr = index;
        this.targetGruopValue = item;
      } else {
        this.targetGr = null;
      }
      console.log(item);
      console.log(index);
    },
    //** */ добавить номер группы
    addGroupNumber(groupNumber) {
      if (groupNumber !== null) {
        this.groupList.push(groupNumber);
      }
    },
    //** */ удаляет выбранную группу по индексу
    deleteGroup() {
      if (this.targetGr !== null) {
        this.groupList.splice(this.targetGr, 1);
      }
      this.targetGr = null;
    },
    //** */ редактирование номера группы из списка
    editGroupNumber(event) {
      if (event !== null) {
        this.groupList[this.targetGr] = event;
        this.targetGr = null;
      } else {
        this.targetGr = null;
      }
    },

    //** ПАГИНАЦИЯ*/

    prevPage() {
      if (this.pageNamber > 0) this.pageNamber--;
    },
    nextPage() {
      if (this.pageNamber < this.pageCount - 1) this.pageNamber++;
    },
    changeStudentSize(value) {
      value > 0 ? (this.size = value) : (this.size = 4);
      this.pageNamber = 0;
    },

    filterStuds(value) {
      // console.log(value);
      this.FilterStudents = value;
    },

    //** Сортировка */
    sortLastName() {
      let student = this.students;
      if (this.revers) {
        student.sort((a, b) => (a.lastname > b.lastname ? 1 : -1));
        this.revers = !this.revers;
      } else {
        student.sort((a, b) => (a.lastname < b.lastname ? 1 : -1));
        this.revers = !this.revers;
      }
      this.students = student;
    },
    sortNumberGroup() {
      let sortGroup = this.students;
      if (this.revers) {
        sortGroup.sort((a, b) => (a.numberGroup > b.numberGroup ? 1 : -1));
        this.revers = !this.revers;
      } else {
        sortGroup.sort((a, b) => (a.numberGroup < b.numberGroup ? 1 : -1));
        this.revers = !this.revers;
      }
      this.students = sortGroup;
    },
  },
  computed: {
    //** Расчитываем общее кол-во страниц */
    PaginateData() {
      const start = this.pageNamber * this.size;
      const end = start + this.size;
      return this.students.slice(start, end);
    },
    //** Отображаем кол-во студентов на страницу */
    pageCount() {
      let l = this.students.length;
      let s = this.size;
      return Math.ceil(l / s);
    },
  },
  components: {
    StudSearchBox,
    TableStudents,
    AddStudentsBox,
    GroupBox,
    PaginationBox,
  },
};
</script>

<style>
body {
  background-color: rgb(247, 255, 245);
}
.main {
  width: 100%;
}
.section {
  display: flex;
}
</style>
