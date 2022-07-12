<template>
  <div class="myList">
    <input type="checkbox" id="cbox1" v-model="toggle" @click="sendTog">
    <label for="cbox1">{{inputValue}}</label>
  </div>  
</template>

<script>
export default {
  name:'myList',
  props: {
    inputValue:String,
    finishTog:Boolean
  },
  data() {
    return {
      toggle:false
    }
  },
  methods: { 
    sendTog(){
      // this.finishTog == true ? this.toggle = true : this.toggle = false;
      this.$emit('func',this.toggle);
    }
  }
}
</script>

<style scoped>
.myList {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
}
input {
  width: 15px;
  height: 15px;
}
label {
  font-size: 15px;
}
</style>