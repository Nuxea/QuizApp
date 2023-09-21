<script setup>
import q from "@/data/quizes.json"
import { ref, watch } from "vue"
import gsap from "gsap"
import Card from "@/components/Card.vue";

const quizes = ref(q)
const search = ref("")

watch(search, () => {
  quizes.value = q.filter(
      quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase())
  )
})

const beforeEnter = (el) => {
  // card-enter-from
  el.style.opacity = 0
  el.style.transform = "translateX(100px)"
}
const enter = (el) => {
  // card-enter-to
  gsap.to(el, {
    x: 0,
    opacity: 1,
    duration: 0.5,
    delay: el.dataset.index * 0.3
  })
}
const afterEnter = () => {

}
</script>

<template>

  <header>
    <h1>Quiz</h1>
    <input v-model.trim="search" type="text" placeholder="Recherche...">
  </header>
  <div class="options-container">
    <TransitionGroup appear @before-enter="beforeEnter" @enter="enter" @afterEnter="afterEnter">
      <Card v-for="(quiz, index) in quizes" :key="quiz.id" :quiz="quiz" :data-index="index" />
    </TransitionGroup>

  </div>

</template>

<style scoped>

header {
  margin: 30px auto 10px auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header h1 {
  font-weight: bold;
  margin-right: 30px;
}

header input {
  border: none;
  background-color: rgba(128,128,128,0.1);
  padding: 10px;
  border-radius: 5px;
  width: 25%;
  color: var(--color-text);
}

.options-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

</style>