<template>
  <div class="myHead">
    <input
      type="text"
      placeholder="请输入你的任务名称,按回车确认"
      @keyup.enter="add"
    />
  </div>
</template>

<script>
import { nanoid } from "nanoid";
import eventBus from "../../evenBus.js";
export default {
  name: "myHead",
  data() {
    return {
      inputValue: JSON.parse(localStorage.getItem("inputValue")) || [],
    };
  },
  methods: {
    add(event) {
      if (event.target.value) {
        const todoObj = {
          id: nanoid(),
          title: event.target.value,
          done: false,
          isEdit: false,
        };
        this.inputValue.unshift(todoObj);
        eventBus.$emit("inputValue", this.inputValue);
        event.target.value = "";
      } else {
        alert("不许输入空值！");
      }
    },
  },
  mounted() {
    eventBus.$on("inputValue", (e) => {
      this.inputValue = e;
    });
  },
  // 深度监视
  watch: {
    inputValue: {
      deep: true,
      handler(val) {
        localStorage.setItem("inputValue", JSON.stringify(val));
      },
    },
  },
};
</script>

<style scoped>
.myHead {
  height: 45px;
}
input {
  width: 330px;
  height: 30px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin: 5px 6px;
}
</style>
