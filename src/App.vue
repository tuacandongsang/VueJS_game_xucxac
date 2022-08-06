<template>
  <div id="app">
    <div class="wrapper clearfix">
      <Player
      v-bind:isWinner="isWinner"
        v-bind:scoresPlayer="scoresPlayer"
        v-bind:activePlayer="activePlayer"
        v-bind:currenScore="currenScore"
      />
      <Control
        v-bind:startGame="startGame"
        v-on:handleNewgame="handleNewgame"
        v-on:handleRollDice="handleRollDice"
        v-on:handlehold="handlehold"
        v-bind:finalScore="finalScore"
        v-on:handleChangeFinalScore="handleChangeFinalScore"
      />
      <Dices v-bind:dices="dices" />
      <ruleVue
        v-bind:openModal="openModal"
        v-on:handleCloseModal="handleCloseModal"
        v-on:handleStart="handleStart"
      />
    </div>

    <!-- <router-view/> -->
  </div>
</template>

<script>
import Player from "./components/Player.vue";
import Control from "./components/Control.vue";
import Dices from "./components/Dices.vue";
import ruleVue from "./components/rule.vue";
export default {
  name: "App",
  data() {
    return {
      activePlayer: 0,
      scoresPlayer: [13, 30],
      currenScore: 10,
      openModal: false,
      startGame: false,
      dices: [5, 4],
      finalScore: 10,
    };
  },
  computed: {
    isWinner() {
      // let { scoresPlayer, finalScore } = this;
      if (this.scoresPlayer[0] >= this.finalScore || this.scoresPlayer[1] >= this.finalScore) {
        this.startGame = false;
        return true;
      }
      return false;
    },
  },
  methods: {
    handleChangeFinalScore(e) {
      const number = parseInt(e.target.value);
      if (isNaN(number)) {
        this.finalScore = "";
      } else {
        this.finalScore = number;
      }
    },
    handlehold() {
      if (this.startGame) {
        this.scoresPlayer[this.activePlayer] =
          this.scoresPlayer[this.activePlayer] + this.currenScore;
        if (!this.isWinner) {
          this.changePlayer();
        }
      } else {
        alert("chua tao tro choi");
      }
    },
    handleNewgame() {
      this.openModal = !this.openModal;
    },
    handleCloseModal(close) {
      this.openModal = close;
    },
    handleStart(close) {
      this.startGame = true;
      this.openModal = close;
      this.activePlayer = 0;
      this.scoresPlayer = [0, 0];
      this.currenScore = 0;
      this.dices = [1, 1];
    },
    handleRollDice() {
      if (this.startGame) {
        const dice1 = Math.floor(Math.random() * 6) + 1;
        const dice2 = Math.floor(Math.random() * 6) + 1;
        this.dices = [dice1, dice2];
        if (dice1 == 1 || dice2 == 1) {
          let player = this.activePlayer;
          setTimeout(function () {
            alert(`nguoi cho so ${player + 1} quay so 1, mat luot ve 0`);
          }, 1000);
          this.changePlayer();
        } else {
          this.currenScore = this.currenScore + dice1 + dice2;
        }
      } else {
        alert("chua tao tro choi");
      }
    },
    changePlayer() {
      this.activePlayer = this.activePlayer == 1 ? 0 : 1;
      this.currenScore = 0;
    },
  },
  components: { Player, Control, Dices, ruleVue },
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

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
    url(../src/assets/back.jpg);
  background-size: cover;
  background-position: center;
  font-family: Lato;
  font-weight: 300;
  position: relative;
  height: 100vh;
  color: #555;
}

.wrapper {
  width: 1000px;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background-color: #fff;
  box-shadow: 0px 10px 50px rgba(0, 0, 0, 0.3);
  overflow: hidden;
}
</style>
