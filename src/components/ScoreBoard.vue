<template>
    <div class="score-board">
      <PlayerScore
        v-for="(player, index) in players"
        :key="index"
        :playerName="player.name"
        :score="player.score"
      />
    </div>
  </template>
  
  <script>
  import PlayerScore from "@/components/PlayerScore.vue";
  
  export default {
    components: {
      PlayerScore
    },
    props: {
      players: Array
    }
  };
  </script>
  
  <style scoped>
  /* Add component styles here */
  </style>
  