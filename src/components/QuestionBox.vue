<template>
   <div class="question-box-container">
      <b-jumbotron>
         <template slot="lead">
          {{ currentQuestion.question }}
         </template>
         <hr class="my-4"/>
         <b-list-group >
            <b-list-group-item 
            v-for="(answer, index) in answers " :key="index"
             @click="selectAnswer(index)"
             :class="
             !answered && selectedIndex === index ? 'selected':
             answered && correctIndex === index ? 'correct':
             answered &&  selectedIndex === index && correctIndex !== index  ? 'incorrect': ''

             ">  
             {{ answer }}
            </b-list-group-item>
         </b-list-group>
         <b-button  @click="submitAnswer" :disabled="selectedIndex === null || answered " variant="primary" href="#">Submit</b-button>
         <b-button @click="next" variant="success" href="#">Next</b-button>
      </b-jumbotron>
   </div>
</template>
<script>
import _ from  "lodash"
export default {
   props:{
      currentQuestion: Object,
      next:Function,
      increment:Function
   },
  data(){
     return{
       selectedIndex: null,
       shuffleAnswers: [],
       answered: false,
       correctIndex: null
     }
  },
   computed:{
      answers(){
         let answers = [...this.currentQuestion.incorrect_answers]
         answers.push(this.currentQuestion.correct_answer)
         return answers
      }
   },
   watch:{
    currentQuestion: {
       immediate:true,
       handler(){
       this.selectedIndex = null,
       this.answered = false,
       this.shuffleAnswer()
       }
    }
    
       
   
   },
    methods:{
      selectAnswer(index){
         this.selectedIndex = index
      },
      submitAnswer(){
       let isCorrect = false
       if(this.selectedIndex === this.correctIndex){
           isCorrect = true
       }
       this.answered = true
       this.increment(isCorrect)
      },
      shuffleAnswer(){
         let answers = [...this.currentQuestion.incorrect_answers, this.currentQuestion.correct_answer]
          this.shuffleAnswers = _.shuffle(answers)
          this.correctIndex = this.shuffleAnswers.indexOf(this.currentQuestion.correct_answer)
      },
   
}

}
</script>

<style scoped>
.list-group{
   margin-bottom: 15px;
}
.list-group-item:hover{
   background-color: #eee;
   cursor: pointer;
}
.btn{
   margin: 0 5px;
}
.selected{
   background-color: lightblue;
}
.correct{
   background-color: lightgreen;
}
.incorrect{
   background-color: rgb(236, 119, 119);
}
</style>