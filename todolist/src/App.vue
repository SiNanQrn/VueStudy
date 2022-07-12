<template>
  <div id="app">
    <myHead></myHead>
    <myBody></myBody>
    <myBottom></myBottom>
  </div>
</template>

<script>
  import myHead from './components/myHead.vue'
  import myBody from './components/myBody.vue'
  import myBottom from './components/myBottom.vue'

export default {
  name: 'App',
  components: {
    myHead,
    myBody,
    myBottom
  }
}
</script>

<style>
#app {
  color: #2c3e50;
  width: 350px;
  /* height: 370px; */
  margin: 40px auto;
  border: 1px solid #dddd;
  background-color: white;
}
</style>
