<script setup>
import {useRoute} from "vue-router";
import quizes from "@/data/quizes.json"

const route = useRoute()
const quizId = parseInt(route.params.id)
const quiz = quizes.find(q => q.id === quizId)

const { quizQuestionsLength, numberOfCorrectAnswers } = defineProps(["quizQuestionsLength", "numberOfCorrectAnswers"])
</script>

<template>
  <header>
    <h2>Résultat...</h2>
    <h4>{{ numberOfCorrectAnswers }} / {{ quizQuestionsLength }}</h4>
  </header>
  <div class="options-container">
    <p v-if="numberOfCorrectAnswers === 10">
      Wouaouh ! C'est un parfait, félicitations !
    </p>
    <p v-if="numberOfCorrectAnswers >= 5 && numberOfCorrectAnswers < 10">
      Bravo, Vous avez fait un très bon score !
    </p>
    <p v-if="numberOfCorrectAnswers >= 0 && numberOfCorrectAnswers < 5">
      Ne vous découragez pas ! Vous pouvez y arriver !
    </p>
    <div class="links-container">
      <a @click="this.$router.go()" class="button">Réessayer</a>
      <RouterLink to="/" class="button">Page d'accueil</RouterLink>
    </div>

  </div>
</template>

<style scoped>
header {
  margin: 30px auto 10px auto;
  display: flex;
  justify-content: space-evenly;
  align-items: center;
}

header h4 {
  font-size: 20px;
  margin-right: 30px;
}

.options-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  margin-top: 40px;
}

.links-container {
  display: flex;
  justify-content: center;
  gap: 20px;
  margin-top: 40px;
}

.button {
  display: flex;
  justify-content: center;
  padding: 15px;
  width: 300px;
  border-radius: 10px;
  background-color: var(--vt-c-text-dark-2);
  color: #3b3b3b;
  font-weight: bold;
  text-decoration: none;
  cursor: pointer;
  transition: 0.3s;
}

.button:hover {
  background-color: #3b3b3b;
  color: var(--vt-c-text-dark-2);
}
</style>