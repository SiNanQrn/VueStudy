<template>
  <div class="myBottom">
    <div class="right">
      <input
        type="checkbox"
        id="finish"
        v-model="finishTog"
        @click="allFinish"
      />
      <label for="finish">已完成{{ finishedNum }}/全部{{ allNum }}</label>
    </div>
    <div class="left">
      <button @click="clearTask">清除已完成任务</button>
    </div>
  </div>
</template>

<script>
import eventBus from "../../evenBus.js";
export default {
  name: "myBottom",
  data() {
    return {
      todoList: [],
      finishedNum: 0,
      allNum: 0,
      finishTog: false,
    };
  },
  methods: {
    clearTask() {
      let newArr = this.todoList.filter((o) => {
        return !o.done;
      });
      // this.todoList.splice(0, this.todoList.length);
      // 置0
      this.finishedNum = 0;
      // 将筛选过的数组共享给其他组件
      eventBus.$emit("inputValue", newArr);
    },
    allFinish() {
      eventBus.$emit("finishTog", this.finishTog);
    },
  },
  mounted() {
    eventBus.$on("inputValue", (e) => {
      this.todoList = e;
      this.allNum = this.todoList.length;
    });
    eventBus.$on("toggle", (o) => {
      this.finishedNum = o;
      if (this.finishedNum == this.allNum && this.allNum) {
        this.finishTog = true;
      } else {
        this.finishTog = false;
      }
    });
  },
};
</script>

<style scoped>
.myBottom {
  width: 350px;
  height: 70px;
  display: flex;
  justify-content: space-between;
  /* background-color: #4444; */
}
.right {
  width: 200px;
  height: 60px;
  line-height: 60px;
}
input {
  width: 15px;
  height: 15px;
}
label {
  font-size: 15px;
}
.left {
  width: 120px;
  height: 60px;
  line-height: 60px;
}
button {
  cursor: pointer;
  height: 40px;
}
</style>
