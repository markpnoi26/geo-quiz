<template>
  <div>
    <b-jumbotron header="QuestionBox">
      <template v-slot:lead>
        {{ currentQuestion.question }}
      </template>

      <hr class="my-4">

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in answers"
          :key="index"
          :class="{answer}"
          @click="checkAnswer(answer)">
          {{ answer }}
        </b-list-group-item>
      </b-list-group>

    </b-jumbotron>
  </div>
</template>

<script>
  export default {
    props: {
      currentQuestion: Object,
      next: Function,
      checkAnswer: Function
    },
    computed: {
      answers: function() {
        let answers = [...this.currentQuestion.incorrect_answers]
        let randomIdx = Math.floor(Math.random() * answers.length+1)
        // randomizes the index of the correct answer
        answers.splice(randomIdx, 0, this.currentQuestion.correct_answer)
        return answers
      }
    }
  }
</script>

<style scoped>
  .answer:hover {
    background: lightgreen;
  }
</style>
