<!-- Baseloop.vue -->
<template>
    <div id="app" class="quiz-container">
      <div v-if="!quizStarted">
        <button @click="startQuiz" class="start-btn">Start Quiz</button>
      </div>
      <div v-else-if="currentQuestionIndex < questions.length" class="question-container">
        <h2>{{ questions[currentQuestionIndex].question }}</h2>
        <ul class="options-list">
          <li v-for="(option, index) in questions[currentQuestionIndex].options" :key="index">
            <input type="radio" :id="'option_' + index" :value="index" v-model="selectedOption">
            <label :for="'option_' + index">{{ option }}</label>
          </li>
        </ul>
        <div class="button-container">
          <button @click="handlePrevQuestion" class="prev-btn" :disabled="currentQuestionIndex === 0">Previous Question</button>
          <button @click="handleNextQuestion" class="next-btn">Next Question</button>
        </div>
      </div>
      <div v-else class="result-container">
        <h2>Quiz Completed!</h2>
        <p>Your score: {{ score }}/{{ questions.length }}</p>
        <button @click="handleRetryQuiz" class="retry-btn">Retry Quiz</button>
      </div>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  
  const quizStarted = ref(false);
  const currentQuestionIndex = ref(0);
  const selectedOption = ref(null);
  const score = ref(0);
  
  const questions = [
    {
      question: 'What is the capital of France?',
      options: ['Berlin', 'Paris', 'Madrid', 'Rome'],
      correctIndex: 1
    },
    {
      question: 'Which planet is known as the Red Planet?',
      options: ['Mars', 'Venus', 'Jupiter', 'Saturn'],
      correctIndex: 0
    },
    {
      question: 'What is the largest mammal?',
      options: ['Elephant', 'Blue Whale', 'Giraffe', 'Hippopotamus'],
      correctIndex: 1
    }
    // Add more questions as needed
  ];
  
  const startQuiz = () => {
    quizStarted.value = true;
  };
  
  const handleNextQuestion = () => {
    if (selectedOption.value !== null) {
      if (selectedOption.value === questions[currentQuestionIndex.value].correctIndex) {
        score.value++;
      }
      currentQuestionIndex.value++;
      selectedOption.value = null;
    }
  };
  
  const handlePrevQuestion = () => {
    if (currentQuestionIndex.value > 0) {
      currentQuestionIndex.value--;
      selectedOption.value = null;
    }
  };
  
  const handleRetryQuiz = () => {
    currentQuestionIndex.value = 0;
    selectedOption.value = null;
    score.value = 0;
  };
  </script>
  
  <style scoped>
  .quiz-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    max-width: 600px;
    margin: 50px auto;
    padding: 20px;
    background-color: #f5f5f5;
    border-radius: 10px;
    box-shadow: 0 0 10px rgba(1, 1, 10, 0.21);
  }
  
  .start-btn {
    background-color: #18248b;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .start-btn:hover {
    background-color: #0fdf1a;
  }
  
  .question-container {
    text-align: center;
  }
  
  .options-list {
    list-style: none;
    padding: 0;
  }
  
  li {
    margin: 10px 0;
  }
  
  .button-container {
    display: flex;
    justify-content: space-between;
    margin-top: 20px;
  }
  
  .prev-btn,
  .next-btn,
  .retry-btn {
    background-color: #18248b;
    color: #fff;
    padding: 10px 20px;
    border: none;
    border-radius: 5px;
    cursor: pointer;
    transition: background-color 0.3s;
  }
  
  .prev-btn:disabled {
    background-color: #23258a;
    cursor: not-allowed;
  }
  
  .prev-btn:hover,
  .next-btn:hover,
  .retry-btn:hover {
    background-color: #0fdf1a;
  }
  
  .result-container {
    text-align: center;
    padding: 20px;
    background-color: #4ca863;
    border-radius: 10px;
    color: #ffffff;
  }
  </style>
  