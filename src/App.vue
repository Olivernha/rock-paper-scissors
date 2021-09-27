<template>
  <div class="wrapper">
    <div class="scoreboard">
      <div class="title">
        <img src="./assets/logo.svg" />
      </div>
      <div class="score">
        <p>SCORE</p>
        <h1>0</h1>
      </div>
    </div>
    <div class="hands" v-show="playing">
      <div class="button paper">
        <div class="icon-bg">
          <img src="./assets/icon-paper.svg" @click.prevent="pickUserHand('paper')"/>
        </div>
      </div>
      <div class="button scissors">
        <div class="icon-bg">
          <img src="./assets/icon-scissors.svg" @click.prevent="pickUserHand('scissors')"/>
        </div>
      </div>
      <div class="button rock">
        <div class="icon-bg">
          <img src="./assets/icon-rock.svg" @click.prevent="pickUserHand('rock')"/>
        </div>
      </div>
    </div>
    <div class="contest">
      <div class="userhand">
        <h1>YOU PICKED</h1>
        <div class="handImageContainer button scissors">
           <div class="icon-bg">
          <img src="./assets/icon-paper.svg" alt="">
           </div>
        </div>
      </div>
      <div class="referee">
        <div class="decision">
          <h1>YOU WIN</h1>
        </div>
        <div class="newGame">PLAY AGAIN</div>
      </div>
      <div class="computerhand">
        <h1>THE HOUSE PICKED</h1>
        <div class="handImageContainer button scissors">
           <div class="icon-bg">
          <img src="./assets/icon-paper.svg" alt="">
           </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  name: "App",
  components: {},
  setup(){
    const playing= ref(false)
    function pickUserHand(hand){
        console.log(hand);
    }
    return {
      pickUserHand,playing
    }
  }
};
</script>

<style>
</style>
