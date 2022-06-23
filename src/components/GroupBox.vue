<template>
  <div class="group-form-block">
    <h3>список групп</h3>
    <ul v-for="(item, index) in groups" :key="index">
      <li
        class="group-item"
        :class="{ active: targetGr === index }"
        @click="targetGroup(item, index)"
        :key="index"
      >
        {{ item }}
      </li>
    </ul>
    <input
      v-model="groupNumber"
      type="number"
      name=""
      placeholder="номер группы"
      @keyup.enter="addGroupNumber"
    />
    <button v-if="targetGr === null" @click="addGroupNumber">добавить</button>
    <button v-if="targetGr !== null" @click="editGroupNumber">изменить</button>
    <button @click="deleteGroup">удалить</button>
  </div>
</template>

<script>
export default {
  name: "AddGroupBox",
  data() {
    return {
      groupNumber: this.targetGruopValue,
      groups: this.groupList,
    };
  },
  props: {
    groupList: Array,
    targetGr: Number,
    targetGruopValue: Number,
  },
  methods: {
    // добавить группу в список групп
    addGroupNumber() {
      this.$emit("addGroupNumber", this.groupNumber);
      this.groupNumber = null;
    },
    // выделить группу из списка
    targetGroup(item, index) {
      this.$emit("targetGroup", item, index);
    },
    deleteGroup() {
      this.$emit("deleteGroup");
      this.groupNumber = null;
    },
    editGroupNumber() {
      this.$emit("editGroupNumber", this.groupNumber);
      this.groupNumber = null;
    },
  },
};
</script>

<style scoped>
li {
  list-style-type: none;
}
.group-form-block {
  width: 320px;
  height: 100%;
  border: 1px solid rgb(56, 56, 56);
}
.active {
  background-color: rgb(122, 254, 85);
}
.group-item:hover {
  cursor: pointer;
}
.group-form-block {
  margin-left: 30px;
  padding: 0 10px 12px 10px;
}
</style>