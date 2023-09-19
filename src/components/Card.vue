<script setup>

import {useRouter} from "vue-router";

const router = useRouter()
const { quiz } = defineProps(['quiz'])

const navigateToQuiz = () => {
  router.push(`/quiz/${quiz.id}`)
}
</script>

<template>
  <div class="card" @click="navigateToQuiz">
    <img :src="quiz.img" alt="">
    <div class="card-text">
      <h2>{{ quiz.name }}</h2>
      <p>{{ quiz.questions.length }} questions</p>
    </div>
  </div>

</template>

<style scoped>
  .card {
    width: 310px;
    overflow: hidden;
    border-radius: 2%;
    box-shadow: 1px 1px 10px rgba(0,0,0,0.5);
    margin: auto auto 35px 20px;
    padding: 0 0 15px 0;
    cursor: pointer;
    text-decoration: none;
    color: var(--vt-c-text-dark-2);
  }

  .card img {
    width: 100%;
    height: 190px;
    margin: 0;
    object-fit: cover;
  }

  .card .card-text {
    padding: 0 15px;
  }

  .card .card-text h2 {
    font-weight: bold;
    text-decoration: none;
    text-align: center;

  }
</style>