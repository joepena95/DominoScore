<template>
    <div class="player-score">
      <h2>{{ playerName }}</h2>
      <p>Score: {{ score }}</p>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      playerName: String,
      score: Number
    }
  };
  </script>
  
  <style scoped>
  /* Add component styles here */
  </style>
  