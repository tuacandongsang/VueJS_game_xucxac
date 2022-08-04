<template>
  <div id="app">
    <div class="wrapper clearfix">
      <Player
        v-bind:scoresPlayer="scoresPlayer"
        v-bind:activePlayer="activePlayer"
        v-bind:currenScore="currenScore"
      />
      <Control
      v-on:handleNewgame="handleNewgame"
      />
      <Dices />
      <ruleVue v-bind:openModal="openModal" />
      
    </div>

    <!-- <router-view/> -->
  </div>
</template>

<script>
import Player from './components/Player.vue';
import Control from './components/Control.vue';
import Dices from './components/Dices.vue';
import ruleVue from './components/rule.vue';
export default {
    name: "App",
    data(){
      return{
        activePlayer: 1 ,
        scoresPlayer:[13 , 30],
        currenScore: 10,
        openModal:false
      }
    },
    methods:{
      handleNewgame(){
        console.log('tuancan');
        this.openModal = !this.openModal
      }
    },
    components: { Player, Control, Dices, ruleVue }
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
