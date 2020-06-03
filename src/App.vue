<template>
  <div id="app">
    <h3 class="animate__animated animate__bounce">The Super Quizz 🧙🏻‍♂️</h3>
    <quizz-panel></quizz-panel>
  </div>
</template>

<script>
import QuizzPanel from '@/components/QuizzPanel.vue';

export default {
  name: 'App',
  components: { 
    QuizzPanel,
  }
}
</script>

<style>
body {
  font-family: sans-serif;
}
#app {
  text-align: center;
  margin-top: 50px;
}
</style>
