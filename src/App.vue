<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const questions = ref([]);
const currentQuestionIndex = ref(0);
const selectedAnswer = ref(null);
const score = ref(0);
const showResults = ref(false);

const fetchQuestions = async () => {
  try {
    const { data } = await axios.get('http://localhost:5000/questions');
    questions.value = data;
  } catch (error) {
    console.error("Error fetching questions:", error);
  }
};

const submitAnswer = async () => {
  if (!selectedAnswer.value) return;

  const response = await axios.post('http://localhost:5000/check-answer', {
    questionId: questions.value[currentQuestionIndex.value].id,
    selectedAnswer: selectedAnswer.value,
  });

  if (response.data.isCorrect) score.value++;

  if (currentQuestionIndex.value < questions.value.length - 1) {
    currentQuestionIndex.value++;
    selectedAnswer.value = null;
  } else {
    showResults.value = true;
  }
};

const restartGame = () => {
  currentQuestionIndex.value = 0;
  selectedAnswer.value = null;
  showResults.value = false
}

onMounted(fetchQuestions);
</script>

<template>
  <div class="p-6 max-w-md mx-auto">
    <div v-if="!showResults">
      <h2 class="text-xl font-bold">Question {{ currentQuestionIndex + 1 }} of {{ questions.length }}</h2>
      <p class="mt-4">{{ questions[currentQuestionIndex]?.question }}</p>

      <div class="mt-4">
        <button 
          v-for="option in questions[currentQuestionIndex]?.options" 
          :key="option"
          @click="selectedAnswer = option"
          class="block w-full px-4 py-2 mt-2 border  rounded cursor-pointer hover:bg-gray-300 hover:bg-gray-100 hover:border-black"
          :class="{ 'bg-gray-400 hover:bg-gray-400' : selectedAnswer === option }"
        >
          {{ option }}
        </button>
      </div>

      <button @click="submitAnswer" class="w-full sm:w-auto mt-4 px-4 py-2 bg-green-500 text-white rounded cursor-pointer ">
        Next
      </button>
    </div>

    <div v-else>
      <h2 class="text-2xl font-bold">Quiz Completed!</h2>
      <p class="mt-4">Your score: {{ score }} / {{ questions.length }}</p>
      <button @click="restartGame" class="mt-4 px-4 py-2 bg-green-500 text-white rounded">
        Play Again
      </button>
    </div>
  </div>
</template>
