<template>
  <div id="app">
    <div class="wrapper clearfix">
      <players
        :isWinner="isWinner"
        :scorePlayer="scorePlayer"
        :activePlayer="activePlayer"
        :currentScore="currentScore"
      />
      <controls
        @handleNewGame="handleNewGame()"
        @handleRollDice="handleRollDice()"
        @handleHoldScore="handleHoldScore()"
        @handleChangeFinalScore="handleChangeFinalScore($event)"
        :finalScore="finalScore"
        :isPlaying="isPlaying"
      />
      <dices :dices="dices" />
      <popup-rule @handleConfirm="handleConfirm()" :isOpenPopup="isOpenPopup" />
    </div>
  </div>
</template>

<script>
import Players from "./components/Players";
import Controls from "./components/Controls";
import Dices from "./components/Dices";
import PopupRule from "./components/PopupRule";

export default {
  name: "app",
  data() {
    return {
      isPlaying: false,
      isOpenPopup: false,
      activePlayer: 0,
      scorePlayer: [0, 0],
      dices: [1, 1],
      currentScore: 0,
      finalScore: ""
    };
  },
  components: {
    Players,
    Controls,
    Dices,
    PopupRule
  },
  computed: {
    isWinner() {
      let { scorePlayer, finalScore } = this;
      if (
        this.isPlaying === true &&
        (scorePlayer[0] >= finalScore || scorePlayer[1] >= finalScore)
      ) {
        this.isPlaying = false;
        return true;
      }
      return false;
    }
  },
  methods: {
    handleChangeFinalScore(e) {
      let num = parseInt(e.target.value);
      if (isNaN(num)) {
        this.finalScore = "";
      } else {
        this.finalScore = num;
      }
    },
    nextPlayer() {
      this.activePlayer = this.activePlayer === 0 ? 1 : 0;
      this.currentScore = 0;
    },
    handleNewGame() {
      this.isOpenPopup = true;
    },
    handleConfirm() {
      if (this.finalScore === "" || this.finalScore === 0) alert("Bạn chưa nhập Final Score");
      else {
        this.isPlaying = true;
        this.activePlayer = 0;
        this.scorePlayer = [0, 0];
        this.currentScore = 0;
        this.dices = [1, 1];
      }
      this.isOpenPopup = false;
    },
    handleHoldScore() {
      if (this.isPlaying === true) {
        let { scorePlayer, activePlayer, currentScore } = this;
        let oldScore = scorePlayer[activePlayer];
        this.$set(this.scorePlayer, activePlayer, oldScore + currentScore);
        if (!this.isWinner) this.nextPlayer();
      } else {
        alert("Vui long nhan vao nut NewGame");
      }
    },

    handleRollDice() {
      if (this.isPlaying == true) {
        //Xoay xuc xac
        let dice1 = Math.round(1 + Math.random() * 5);
        let dice2 = Math.round(1 + Math.random() * 5);
        this.dices = [dice1, dice2];

        if (dice1 === 1 || dice2 === 1) {
          setTimeout(() => {
            alert(
              `Nguoi choi Player ${this.activePlayer +
                1} đã quay trúng số 1. Rất tiếc!`
            );
            this.nextPlayer();
          }, 10);
        } else {
          this.currentScore += dice1 + dice2;
        }
      } else {
        alert("Vui long nhan vao nut NewGame");
      }
    }
  }
};
</script>

<style>
</style>
