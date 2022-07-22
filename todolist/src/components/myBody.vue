<template>
  <div class="myBody">
    <myList
      :inputValue="item"
      v-for="item in todoEven"
      :key="item.id"
      @func="getChecked"
    />
  </div>
</template>

<script>
import myList from "../components/myList.vue";
import eventBus from "../../evenBus.js";
export default {
  name: "myBody",
  data() {
    return {
      // 代办事项
      todoEven: {},
      // 每个事项是否打勾
      check: "",
      // 打勾个数
      checkedNum: 0,
    };
  },
  components: {
    myList,
  },
  methods: {
    getChecked(o) {
      this.check = o;
      this.check === true ? this.checkedNum++ : this.checkedNum--;
      eventBus.$emit("toggle", this.checkedNum);
    },
  },
  mounted() {
    eventBus.$on("inputValue", (e) => {
      this.todoEven = e;
    });
    eventBus.$on("finishTog", (e) => {
      this.todoEven.forEach((o) => (o.done = !e));
      console.log("this.todoEven", this.todoEven);
    });
    eventBus.$on("count", (e) => {
      this.checkedNum = e;
    });
  },
};
</script>

<style>
.myBody {
  width: 340px;
  margin: 0 5px;
}
</style>
