<script setup>
const emit = defineEmits(["selectOption"])
const { question } = defineProps(['question'])

const emitSelectedOption = (isCorrect) => {
  emit("selectOption", isCorrect)
}
</script>

<template>
  <div class="question-container">
    <h1 class="question">{{ question.text }}</h1>
  </div>
  <div class="options-container">
    <div v-for="option in question.options" :key="option.id" @click="emitSelectedOption(option.isCorrect)" class="option">
      <p class="option-label">{{ option.label }}</p>
      <div class="option-value">
        <p>{{ option.text }}</p>
      </div>
    </div>
  </div>
</template>

<style scoped>
.question-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 40px;
}

.question{
  font-size: 20px;
  margin-bottom: 20px;
}

.option {
  display: flex;
  margin-bottom: 20px;
  cursor: pointer;
}

.option-label {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 50px;
  height: 50px;
  font-size: 30px;
  background-color: #fff;
  color: #3b3b3b;
  border-radius:15px 0 0 15px;
}

.option-value {
  width: 100%;
  font-size: 30px;
  padding: 0 20px;
  background-color: rgba(59, 59, 59, 0.82);
  border-radius: 0 15px 15px 0;

}
</style>