<script setup>
import Question from "@/components/Question.vue";
import QuizHeader from "@/components/QuizHeader.vue";
import quizes from "@/data/quizes.json"
import {useRoute} from "vue-router";
import {computed, ref} from "vue";
import Result from "@/components/Result.vue";

const route = useRoute()
const quizId = parseInt(route.params.id)
const quiz = quizes.find(q => q.id === quizId)
const currentQuestionIndex = ref(0)
const numberOfCorrectAnswers = ref(0)
const showResults = ref(false)

// const questionStatus = ref(`${currentQuestionIndex.value}/${quiz.questions.length}`)
//
// watch(() => currentQuestionIndex.value, () => {
//   questionStatus.value = `${currentQuestionIndex.value}/${quiz.questions.length}`
// })

const questionStatus = computed(() => `${currentQuestionIndex.value}/${quiz.questions.length}`)

const barPercentage = computed(() => {
  return `${currentQuestionIndex.value/quiz.questions.length * 100}%`
})

const onOptionSelected = (isCorrect) => {
  if (isCorrect) {
    numberOfCorrectAnswers.value++
  }

  if (quiz.questions.length - 1 === currentQuestionIndex.value) {
    showResults.value = true
  }
  currentQuestionIndex.value++
}
</script>

<template>
  <QuizHeader :questionStatus="questionStatus" :barPercentage="barPercentage" />
  <div>
    <Question v-if="!showResults" :question="quiz.questions[currentQuestionIndex]" @selectOption="onOptionSelected" />
    <Result v-else :quizQuestionsLength="quiz.questions.length" :numberOfCorrectAnswers="numberOfCorrectAnswers" />
  </div>
</template>

<style scoped>

</style>