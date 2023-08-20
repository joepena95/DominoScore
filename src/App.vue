<template>
  <div id="app">
    <div class="team-names">
      <div class="team-name">
        <input v-model="players[0].name" class="team-input" />
      </div>
      <div class="divider"></div>
      <div class="team-name">
        <input v-model="players[1].name" class="team-input" />
      </div>
    </div>
    <ScoreBoard :players="players" />
    <div class="input-container">
      <div class="input-team">
        <label>{{ players[0].name }}</label>
        <input v-model.number="team1Score" type="number" />
        <button @click="addScores('TEAM1')">Add Score</button>
        <p>Total: {{ players[0].score }}</p>
      </div>
      <div class="input-team">
        <label>{{ players[1].name }}</label>
        <input v-model.number="team2Score" type="number" />
        <button @click="addScores('TEAM2')">Add Score</button>
        <p>Total: {{ players[1].score }}</p>
      </div>
      <button @click="resetScores">Reset Scores</button>
    </div>
    <p v-if="winner">{{ winner }} wins!</p>
  </div>
</template>

<script>
import ScoreBoard from "@/components/ScoreBoard.vue";

export default {
  name: "App",
  components: {
    ScoreBoard
  },
  data() {
    return {
      players: [
        { name: "TEAM1", score: 0 },
        { name: "TEAM2", score: 0 }
      ],
      team1Score: 0,
      team2Score: 0
    };
  },
  computed: {
    winner() {
      if (this.players[0].score >= 500) {
        return this.players[0].name;
      } else if (this.players[1].score >= 500) {
        return this.players[1].name;
      }
      return null;
    }
  },
  methods: {
    addScores(teamName) {
      const teamIndex = teamName === "TEAM1" ? 0 : 1;
      const scoreToAdd = teamName === "TEAM1" ? this.team1Score : this.team2Score;
      this.players[teamIndex].score += scoreToAdd;
      this.checkAndAwardPrizes(teamIndex);
      this.team1Score = 0;
      this.team2Score = 0;
    },
    checkAndAwardPrizes(teamIndex) {
      const teamTotal = this.players[teamIndex].score;
      const prizeScores = [100, 75, 50, 25];
      if (teamTotal <= 4) {
        this.players[teamIndex].score += prizeScores[teamTotal - 1];
      }
    },
    resetScores() {
      this.players.forEach(player => {
        player.score = 0;
      });
      this.team1Score = 0;
      this.team2Score = 0;
    }
  }
};
</script>

<style>
.team-names {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 20px;
}

.team-name {
  font-size: 20px;
  margin: 0 10px;
}

.team-input {
  width: 100px;
  text-align: center;
}

.divider {
  height: 100px;
  width: 4px;
  background-color: black;
}

.input-container {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  margin-top: 20px;
}

.input-team {
  margin: 10px;
}
</style>




