<template>
  <div class="myHead">
    <input 
      type="text" 
      placeholder=" 请输入你的任务名称,按回车确认"
      @keyup.enter="inputVal"
    >
  </div>  
</template>

<script>
import eventBus from '../../evenBus.js'
export default {
  name:'myHead',
  data(){
    return{
      inputValue:[]
    }
  },
  methods: {
    inputVal(event){
      if(event.target.value){
        this.inputValue.push(event.target.value);
        eventBus.$emit('inputValue',this.inputValue);
        event.target.value = ""
      }else{
        alert("不许输入空值！");
      }
     
    }
  }
}
</script>

<style>
.myHead {
  height: 45px;
  /* background-color:red; */
}
input {
  width: 330px;
  height: 30px;
  border: 1px solid #ddd;
  border-radius: 5px;
  margin: 5px 6px;
}
</style>