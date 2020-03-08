<template>
  <div>
    <b-jumbotron header="Your Final Stats">
      <template v-slot:lead>
        You have answered all the questions and got {{correct}} out of 10 ({{ percentage }}%) correctly.
        <div>
          <b-button
            @click='restartQuiz'
            variant="success">
            Restart the Quiz
            </b-button>
        </div>
      </template>

    </b-jumbotron>
  </div>
</template>

<script>
  export default {
    props: {
      restartQuiz: Function,
      correct: Number
    },
    computed: {
      percentage() {
        let percentage = (this.correct/10)*100
        return percentage
      }
    }
  }
</script>

<style scoped>
  .answer:hover {
    background: lightgreen;
  }
</style>
