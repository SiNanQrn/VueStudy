<template>
  <div class="myBody">
    <myList 
      :inputValue='item'  
      :finishTog='finishTog'
      v-for="(item,index) in todoEven" 
      :key="index" 
      @func="getTog" />
  </div>  
</template>

<script>
import myList from '../components/myList.vue'
import eventBus from '../../evenBus.js'
export default {
  name:'myBody',
  data(){
    return{
      // 代办事项
      todoEven:'',
      // 每个事项是否打勾
      istog:'',
      // 打勾个数
      togNum:0,
      // 
      finishTog:false
    }
  },
  components: {
    myList
  },
  methods: {
    getTog(data){
      this.istog = data;  
      this.istog === false ? this.togNum++ : this.togNum--;  
      eventBus.$emit('toggle',this.togNum);
      console.log('qrn',this.togNum);
    }
  },
  mounted(){
    eventBus.$on('inputValue',(e)=>{
      this.todoEven = e
    });
    eventBus.$on('finishTog',(o)=>{
      this.finishTog = o
      // console.log("this.finishTog", this.finishTog);
      // if(this.finishTog === false){
        this.getTog(this.finishTog);
      // }
     
      // this.finishTog === false ? this.istog = false : this.istog = true; 

    });
  },
}
</script>

<style>
.myBody {
  width: 340px;
  /* height: 255px; */
  margin: 0 5px;
  /* background-color:rgb(0, 255, 128); */

}
</style>