<template>
  <div>
    <h1>Welcome to Chikhalifa App</h1>
    <!-- <h1>{{ msg }}</h1> -->
  <b-nav tabs>
   <!-- <h1>{{ msg }}</h1>  -->
    <b-nav-item disabled><b>Chikhalifa Quiz App</b></b-nav-item>
    <b-nav-item disabled>Number of Correct Question:{{numCorrect}}/{{numTotal}}</b-nav-item>
    <!-- <b-nav-item>Another Link</b-nav-item>
    <b-nav-item disabled>Disabled</b-nav-item> -->
  </b-nav> 
</div>   
</template>
<script>
export default {
  props:[
    'numCorrect',
    'numTotal'
  ]
    
  
}
</script>
<style>
h1 {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>