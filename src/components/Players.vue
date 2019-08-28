<template>
  <div class="wrapper-layer">
    <div
      class="player-panel"
      :class="{
        active: activePlayer == 0 && !this.isWinner,
        winner: activePlayer == 0 && this.isWinner
        }"
    >
      <div class="player-name">{{getNamePlayer(0)}}</div>
      <div class="player-score">{{scorePlayer[0]}}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">{{activePlayer == 0 ? currentScore : 0}}</div>
      </div>
    </div>

    <div
      class="player-panel"
      :class="{
        active: activePlayer == 1 && !this.isWinner,
        winner: activePlayer == 1 && this.isWinner}"
    >
      <div class="player-name">{{getNamePlayer(1)}}</div>
      <div class="player-score">{{scorePlayer[1]}}</div>
      <div class="player-current-box">
        <div class="player-current-label">Current</div>
        <div class="player-current-score">{{activePlayer == 1 ? currentScore : 0}}</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "players",
  props: {
    scorePlayer: { type: Array, default: [0, 0] },
    currentScore: { type: Number, default: 0 },
    activePlayer: { type: Number, default: 0 },
    isWinner: { type: Boolean, default: false }
  },
  data() {
    return {};
  },
  methods: {
    getNamePlayer(index) {
      let defaultName = "Player" + (index + 1);

      if (this.activePlayer == index && this.isWinner == true)
        defaultName = "Winner!";
      return defaultName;
    }
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.clearfix::after {
  content: "";
  display: table;
  clear: both;
}

body {
  background-image: linear-gradient(
      rgba(62, 20, 20, 0.4),
      rgba(62, 20, 20, 0.4)
    ),
    url("/public/assets/back.jpg");
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}
</style>