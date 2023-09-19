<script setup>
import q from "@/data/quizes.json"
import { ref, watch } from "vue"
import Card from "@/components/Card.vue";

const quizes = ref(q)
const search = ref("")

watch(search, () => {
  quizes.value = q.filter(
      quiz => quiz.name.toLowerCase().includes(search.value.toLowerCase())
  )
})
</script>

<template>

  <header>
    <h1>Quiz</h1>
    <input v-model.trim="search" type="text" placeholder="Recherche...">
  </header>
  <div class="options-container">
    <Card v-for="quiz in quizes" :key="quiz.id" :quiz="quiz" />
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