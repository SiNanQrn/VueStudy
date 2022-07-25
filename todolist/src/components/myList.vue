<template>
  <div class="myList">
    <div class="left">
      <input
        class="checkInput"
        type="checkbox"
        id="cbox"
        :checked="inputValue.done"
        @change="handleCheck(inputValue)"
      />
      <label v-show="!todo.isEdit" for="cbox">{{ inputValue.title }}</label>
      <input
        type="text"
        v-show="todo.isEdit"
        :value="inputValue.title"
        @blur="handleBlur($event)"
        ref="inputTitle"
      />
    </div>

    <div>
      <button class="btn btn-edit" @click="editTask(inputValue.id)">
        编辑
      </button>
      <button class="btn btn-danger" @click="deleteTask(inputValue.id)">
        删除
      </button>
    </div>
  </div>
</template>

<script>
import { nextTick } from 'vue';
export default {
  name: "myList",
  props: ["inputValue", "finishTog"],
  data() {
    return {
      todo: {},
      checked: false,
    };
  },
  methods: {
    // 打勾
    handleCheck(o) {
      o.done = !o.done;
      this.$emit("func", o.done);
    },
    // 删除
    deleteTask(e) {
      this.$emit("delete", e);
    },
    // 编辑
    editTask() {
      this.todo = this.inputValue;
      this.todo.isEdit = true;
      nextTick(()=>{
        this.$refs.inputTitle.focus();
      })
      console.log("inputValue", this.todo.isEdit);
    },
    // 失焦
    handleBlur(e) {
      this.todo.isEdit = false;
      // 校验
      if(e.target.value == ''){
        alert('不得输入空值！');
        return;
      }
      this.$emit("updateVal", this.todo.id, e.target.value);
    },
  },
};
</script>

<style scoped>
.myList {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  display: flex;
  justify-content: space-between;
}
.myList:hover {
  background-color: rgba(162, 180, 190, 0.407);
}
.left {
  width: 230px;
}
.checkInput {
  width: 15px;
  height: 15px;
}
label {
  font-size: 15px;
}
button {
  width: 50px;
  height: 25px;
  margin-top: 7px;
  /* background-color: brown; */
}
.btn-edit {
  margin-right: 5px;
  color: rgb(243, 243, 243);
  background-color: #77adef;
  border: 1px solid #4499e8;
}
.btn-danger {
  color: rgb(243, 243, 243);
  background-color: #da4f49;
  border: 1px solid #bd3d2f;
}
</style>
