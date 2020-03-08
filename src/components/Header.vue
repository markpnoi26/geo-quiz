<template>
  <div>
    <b-nav tabs
      v-if="currentIndex < 11">
      <b-nav-item disabled> Geography Quick Quiz </b-nav-item>
      <b-nav-item disabled> Questions: {{ currentIndex }}/10 </b-nav-item>
      <b-nav-item disabled> Correct Answer: {{ correct }}/10 </b-nav-item>
    </b-nav>
  </div>
</template>

<script>
  export default {
    props: {
      currentIndex: Number,
      correct: Number
    }
  }
</script>
