<template>
  <div class="myList">
    <input
      type="checkbox"
      id="cbox1"
      :toggle="checked"
      @change="handleCheck(inputValue)"
    />
    <label for="cbox1">{{ inputValue.title }}</label>
  </div>
</template>

<script>
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
    handleCheck(o) {
      o.done = !o.done;
      this.$emit("func", o.done);
    },
    // sendTog() {
    //   // this.finishTog == true ? this.toggle = true : this.toggle = false;
    //   this.$emit("func", this.toggle);
    // },
  },
  mounted() {
    // this.checked = !this.finishTog;
    this.checked = true;
    // this.todo = this.inputValue;
    // console.log("this.todo", this.todo);
    // console.log("this.finishTog", this.finishTog);
  },
  updated() {
    // this.todo.done = !this.finishTog;
    // console.log("this.todo", this.todo);
  },
};
</script>

<style scoped>
.myList {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
}
.myList:hover {
  background-color: rgba(162, 180, 190, 0.407);
}
input {
  width: 15px;
  height: 15px;
}
label {
  font-size: 15px;
}
</style>
