<template>
<body>
  <div class="game-screen">
      <!-- <div class="background1" style="margin-top: 19vh;"> -->
    <div style="color: white; font-family: myFirstFont">Welcome to Animatch!</div>
    <div style="color: white; font-family: myFirstFont">Points Earned: {{ this.score }}</div>
    <!-- <div>{{ store.state.userEmail }}</div> -->
    <!-- <div>{{store.state.userEmail}}</div> -->
    <!-- <canvas ref="input" style="height:1000px; width:1000px;">Test</canvas> -->
      <ion-phaser
        v-bind:game.prop="game"
        v-bind:initialize.prop="initialize"
      />
      <div style="color: white; font-family: myFirstFont">Match the Animals to Win!</div>
      <div style="color: white; font-family: myFirstFont">Use arrow keys to move character and click [spacebar] to peek into the crates.</div>
  </div>
</body>
</template>

<script>

import Phaser from 'phaser';
import AlzheimersPreloader from '../AlzhGame_files/preloader';
import AlzheimersGame from '../AlzhGame_files/Game';
import AlzheimersStart from '../AlzhGame_files/startScreen';
import AlzheimersEducation from '../AlzhGame_files/educationalSnippet';
import eventsCenter from '../AlzhGame_files/EventsCenter';
// import { inject } from 'vue';

// var input;

export default {
  name: 'AlzheimersGame',
  beforeCreate() {
    if (window.localStorage.getItem("userInformation") === null) {
      this.$router.push('/login');
    }
  },
  created: function() {
    this.initUpdates(this);
  },
  // setup() {
  // const store = inject('store');
  //   return {
  //     store
  //   }
  // },
  data: function() {
    return {
      score: 0,
      initialize: true,
      game: {
        width: "80%",
        height:"75%",
        type: Phaser.AUTO,
        physics: {
          default: 'arcade',
          arcade: {
            debug: false,
            gravity: { y: 0}
          }
        },
        scene: [AlzheimersStart, AlzheimersPreloader, AlzheimersGame, AlzheimersEducation], // first scene is auto run
        scale: {
          // mode: Phaser.Scale.FIT,
          // autoCenter: Phaser.Scale.CENTER_BOTH,
        },
      }
    }
  },
  methods: {
    // sayHello: (vm) => console.log(vm.initialize),
    initUpdates: function () {
      eventsCenter.on('score', this.generateUpdateScore(this), this);
    },
    generateUpdateScore: (vm) => {
      // console.log("gen");
      // console.log(input);
      return (updated_score) => {
        vm.score = updated_score;
      }
    },
  },
  // onCreate() {
  //     this.$router.push('/games/alzh')
  //   }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@font-face {
  font-family: myFirstFont;
  src: url('../fonts/PressStart2P-Regular.ttf');
}
@font-face {
  font-family: mySecondFont;
  src: url('../fonts/IndieFlower-Regular.ttf');
}
  .special-jumbotron {
    height: "100vh";
    width: "100vw";
  }

  .background1 {
    background-image: url('../assets/snakeBackground.jpg');
    width:100%;
    height:100%; 
    background-size: cover;
  }

body{
  background-image: linear-gradient(to bottom right, #4a8798b1, #839dd0,#d25091c2);
  /* background-position: center center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover; */
  /* height: 100vh;
  width: 100vw; */

}

/* .header1{ */
  /* font-family:myFirstFont; */
  /* padding-top:20px; */
  /* font-size:30px; */
  /* font-weight:bold; */
/* } */

/* .header2{ */
  /* font-family:mySecondFont; */
  /* font-size:30px; */
/* } */

.game-screen {
  display:flex;
  flex-direction: column;
  justify-content: center;
  height: 100vh;
}
</style>
