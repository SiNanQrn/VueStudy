<template>
  <div class="myList">
    <div>
      <input
        type="checkbox"
        id="cbox"
        :checked="inputValue.done"
        @change="handleCheck(inputValue)"
      />
      <label for="cbox">{{ inputValue.title }}</label>
    </div>
    <button @click="deleteTask(inputValue.id)">删除</button>
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
    deleteTask(e) {
      console.log('e',e);
     this.$emit("delete", e);
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
input {
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
</style>
