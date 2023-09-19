<script setup>
import {useRoute} from "vue-router";
import quizes from "@/data/quizes.json"

const route = useRoute()
const quizId = parseInt(route.params.id)
const quiz = quizes.find(q => q.id === quizId)

const { questionStatus, barPercentage } = defineProps(["questionStatus", "barPercentage"])
</script>

<template>
  <header>
    <h1>{{ quiz.name }}</h1>
    <h4>Question {{ questionStatus }}</h4>
    <div class="bar">
      <div class="completion" :style="{ width: barPercentage }"></div>
    </div>
  </header>
</template>

<style scoped>
header {
  margin: 30px auto 10px auto;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

header h1 {
  font-size: 30px;
  margin-right: 30px;
}

header h4 {
  font-size: 20px;
  margin-right: 30px;
}

.bar {
  width: 300px;
  height: 50px;
  border: 3px solid #fff;
  border-radius: 10px;
}

.completion {
  height: 100%;
  width: 0;
  background-color: #fff;
}
</style>