<template>
  <div class="myBody">
    <myList
      :finishTog="finishTog"
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
      finishTog: false,
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
      console.log("this.todoEven", this.todoEven);
    });
    eventBus.$on("finishTog", (e) => {
      this.finishTog = e;
      // console.log("勾选", e);
      // this.todoEven.forEach((o) => (o.done = !e));
      // console.log("this.todoEven", this.todoEven);
    });
  },
};
</script>

<style>
.myBody {
  width: 340px;
  /* height: 255px; */
  margin: 0 5px;
  /* background-color:rgb(0, 255, 128); */
}
</style>
