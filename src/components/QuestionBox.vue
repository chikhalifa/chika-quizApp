<template>
 <div>
  <b-jumbotron header="Chikhalifa Quiz App" lead="Bootstrap v4 Components for Vue.js 2">
   <template v-slot:lead>
      {{currentQuestion.question}}
    </template>

    <hr class="my-4">
    <b-list-group>
  <b-list-group-item v-for="(answer, index) in answers" :key="index" 
   @click.prevent="selectAnswer(index)"
   :class="answerClass(index)"
   >  {{answer}}
   
  </b-list-group-item>
  
</b-list-group>

    <p  > 
    
    </p>

    <b-button variant="primary" 
    @click="submitAnswer"
    :disabled="selectedIndex===null || answered"
    >
      Submit</b-button>
    <b-button @click="next" variant="success" href="#">Next</b-button>
  </b-jumbotron>
</div>
</template>
<script>
import _ from 'lodash'
export default {
props: {
currentQuestion: Object,
next: Function,
increment:Function
}  ,
data: function(){
  return{
    selectedIndex: null,
    correctIndex:null,
    shuffledAnswers:[],
    answered:false
  }
},

watch:{
 currentQuestion:{

 immediate:true,
 handler(){
 this.selectedIndex=null
 this.answered =false
this.shuffleAnswers()

 }
//  (){
// 
 } 
},
computed :{
  answers(){
    let answers =[...this.currentQuestion.incorrect_answers]
    answers.push(this.currentQuestion.correct_answer)
    return  answers
  }
},
methods :{
selectAnswer(index){
  this.selectedIndex= index
  // console.log(index)
},
shuffleAnswers(){
 let answers =[...this.currentQuestion.incorrect_answers,this.currentQuestion.correct_answers]
 this.shuffledAnswers = _.shuffle(answers)
 this.correctIndex= this.shuffledAnswers.indexOf(this.currentQuestion.correct_answers)
},
answerClass(index){
  let answerClass=''
  if( !this.answered && this.selectedIndex=== index ){
    answerClass='selected'
  }
  else if (this.answered && this.correctIndex === index) {
    answerClass='correct'
  } else if(this.answered && this.selectedIndex=== index && this.correctIndex !== index) {
   answerClass='incorrect' 
  } 
  return answerClass

},
submitAnswer(){
  let isCorrect =false
  if(this.selectedIndex===this.correctIndex){
    isCorrect = true
  }
  this.answered =true
  this.increment(isCorrect)
},

// mounted (){
// this.shuffleAnswers()
// },
}

}

</script>
<style scoped>
.list-group{
  margin-bottom: 15 px;
}
.list-group-item:hover{
  background:gray;
  cursor:pointer;
}
.selected{
  background-color:lightblue;
}
.correct{
  background-color:lightgreen
}
.incorrect{
  background-color:red;
}
.btn{
margin :0 5px;
}
</style>