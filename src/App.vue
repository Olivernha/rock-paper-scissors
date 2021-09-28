<template>
  <div class="wrapper">
    <div class="scoreboard">
      <div class="title">
        <img src="./assets/logo.svg" />
      </div>
      <div class="score">
        <p>SCORE</p>
        <h1>{{ SCORE }}</h1>
      </div>
    </div>
    <div class="hands" v-if="!playing">
      <div class="button paper" @click.prevent="pickUserHand('paper')">
        <div class="icon-bg">
          <img src="./assets/icon-paper.svg" />
        </div>
      </div>
      <div class="button scissors" @click.prevent="pickUserHand('scissors')">
        <div class="icon-bg">
          <img src="./assets/icon-scissors.svg" />
        </div>
      </div>
      <div class="button rock" @click.prevent="pickUserHand('rock')">
        <div class="icon-bg">
          <img src="./assets/icon-rock.svg" />
        </div>
      </div>
    </div>
    <div class="contest" v-else>
      <div class="userhand">
        <h1>YOU PICKED</h1>
        <div
          class="handImageContainer button"
          :style="{ backgroundImage: bgColor, boxShadow: boxShadow }"
        >
          <div class="icon-bg">
            <img :src="image" alt="" />
          </div>
        </div>
      </div>
      <div class="referee">
        <div class="decision">
          <h1>{{ decision }}</h1>
        </div>
        <div class="newGame" @click.prevent="restartGame">PLAY AGAIN</div>
      </div>
      <div class="computerhand">
        <h1>THE HOUSE PICKED</h1>
        <div
          class="handImageContainer button"
          :style="{ backgroundImage: cBgColor, boxShadow: cBoxShadow }"
        >
          <div class="icon-bg">
            <img :src="cImage" alt="" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, ref, toRefs } from "vue";
export default {
  name: "App",
  setup() {
    let bgColor, boxShadow, img;
    const playing = ref(false);
    const SCORE = ref(0);
    const decision = ref(null);
    const userPick = reactive({
      image: null,
      bgColor: null,
      boxShadow: null,
    });
    const computerPick = reactive({
      cImage: null,
      cBgColor: null,
      cBoxShadow: null,
    });
    function colorGenerate(hand) {
      if (hand == "scissors") {
        img = require(`./assets/icon-${hand}.svg`);
        bgColor = "linear-gradient(#ec9e0e, #eca922)";
        boxShadow = "0 7px 0 0 #d39312";
      } else if (hand == "rock") {
        img = require(`./assets/icon-${hand}.svg`);
        bgColor = " linear-gradient(#dc2e4e, #dd405d)";
        boxShadow = "0 7px 0 0 #c32240";
      } else if (hand == "paper") {
        img = require(`./assets/icon-${hand}.svg`);
        bgColor = " linear-gradient(#4865f4, #5671f5)";
        boxShadow = "0 7px 0 0 #0d2fd9";
      }
      return { bgColor, boxShadow, img };
    }
    function pickComputerHand(hand) {
      let hands = ["rock", "scissors", "hand"];
      let cpHands = hands[Math.floor(Math.random() * hands.length)];

      const { bgColor, boxShadow, img } = colorGenerate(cpHands);
      computerPick.cImage = img;
      computerPick.cBgColor = bgColor;
      computerPick.cBoxShadow = boxShadow;
      referee(hand, cpHands);
    }
    function pickUserHand(hand) {
      pickComputerHand(hand);
      playing.value = true;

      const { bgColor, boxShadow, img } = colorGenerate(hand);
      userPick.image = img;
      userPick.bgColor = bgColor;
      userPick.boxShadow = boxShadow;
    }

    function referee(userHand, cpHand) {
      console.log(userHand, cpHand);
      if (userHand == "paper" && cpHand == "scissors") {
        setDecision("YOU LOSE!");
      }
      if (userHand == "paper" && cpHand == "rock") {
        setDecision("YOU WIN!");
        setScore(SCORE.value + 1);
      }
      if (userHand == "paper" && cpHand == "paper") {
        setDecision("It's a tie!");
      }
      if (userHand == "rock" && cpHand == "scissors") {
        setDecision("YOU WIN!");
        setScore(SCORE.value + 1);
      }
      if (userHand == "rock" && cpHand == "paper") {
        setDecision("YOU LOSE!");
      }
      if (userHand == "rock" && cpHand == "rock") {
        setDecision("It's a tie!");
      }
      if (userHand == "scissors" && cpHand == "scissors") {
        setDecision("It's a tie!");
      }
      if (userHand == "scissors" && cpHand == "rock") {
        setDecision("YOU LOSE!");
      }
      if (userHand == "scissors" && cpHand == "paper") {
        setDecision("YOU WIN!");
        setScore(SCORE.value + 1);
      }
    }
    function setDecision(d) {
      decision.value = d;
    }
    function setScore(newScore) {
      SCORE.value = newScore;
    }
    function restartGame() {
      playing.value = false;
    }
    return {
      pickUserHand,
      playing,
      ...toRefs(userPick),
      ...toRefs(computerPick),
      SCORE,
      decision,
      restartGame,
    };
  },
};
</script>

<style>
</style>
