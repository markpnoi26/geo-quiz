<template>
  <div id="app">
    <Header
      :currentIndex="counter"
      :correct="correct"
    />

    <b-container class="bv-example-row">
      <b-row>
        <b-col sm="6" offset="3">
          <QuestionBox
            v-if="questions[index] !== undefined && index !== 11"
            :currentQuestion="questions[index]"
            :checkAnswer="checkAnswer"
            :next="next"/>
          <StatsBox
            v-if="index === 10"
            :correct="correct"
            :restartQuiz='restartQuiz'
            />
        </b-col>
      </b-row>

    </b-container>
  </div>
</template>

<script>

import Header from './components/Header.vue'
import QuestionBox from './components/QuestionBox.vue'
import StatsBox from './components/StatsBox.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuestionBox,
    StatsBox
  },
  data() {
    return {
      questions: [],
      index: 0,
      counter: 1,
      correct: 0
    }
  },
  methods: {
    next: function() {
      this.index++,
      this.counter++
    },
    checkAnswer: function(answer) {
      if (this.questions[this.index].correct_answer === answer) {
        this.correct++
      }
      this.next()
    },
    restartQuiz: function() {
      this.index = 0
      this.counter = 1
      this.correct = 0
      fetch('https://opentdb.com/api.php?amount=10&category=22&difficulty=easy')
        .then(response => response.json())
        .then(json => {
          this.questions = json.results
        })
        .catch(err => console.log(err))
    }
  },
  mounted: function (){
    fetch('https://opentdb.com/api.php?amount=10&category=22&difficulty=easy')
      .then(response => response.json())
      .then(json => {
        this.questions = json.results
      })
      .catch(err => console.log(err))
  }
}

</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
