<template>
  <div id="container">
    <div id="bot-placeholder">
      <img :src="playerImage">
    </div>
    <div id="you-placeholder">
      <img :src="botImage">
    </div>
    <div id="buttons-container">
      <div id="btn-paper" @click="pick(1)"></div>
      <div id="btn-scissor" @click="pick(2)"></div>
      <div id="btn-rock" @click="pick(3)"></div>
    </div>
  </div>
</template>
 
<script>
export default {
  name: 'App',
  data() {
    return {
      playerSelected: 0,
      botSelected: 0,
    }
  },
  methods: {
    pick(selected) {
      // record player's selection
      this.playerSelected = selected;

      // generate a random number from 1 to 3
      this.botSelected = Math.ceil(Math.random() * 3);
    }
  },
  computed: {
    playerStatus() {
      if (this.playerSelected === this.botSelected) {
        return 'draw'; // draw
      } else if (
        this.playerSelected === 1 && this.botSelected === 3 || 
        this.playerSelected === 2 && this.botSelected === 1 || 
        this.playerSelected === 3 && this.botSelected === 2
      ) {
        return 'win'; // win
      } else {
        return 'lose'; // lose
      }
    },
    botStatus() {
      if (this.playerStatus === 'draw') {
        return 'draw';
      } else if (this.playerStatus === 'win') {
        return 'lose';
      } else {
        return 'win';
      }
    },
    playerImage() {
      const selectedToSymbol = [];
      selectedToSymbol[1] = 'paper';
      selectedToSymbol[2] = 'scissor';
      selectedToSymbol[3] = 'rock';

      if (this.playerSelected === 0) {
        return "/images/Placeholder-You.png";
      }

      return `/images/${selectedToSymbol[this.playerSelected]}-${this.playerStatus}.png`;
    },
    botImage() {
      const selectedToSymbol = [];
      selectedToSymbol[1] = 'paper';
      selectedToSymbol[2] = 'scissor';
      selectedToSymbol[3] = 'rock';

      if (this.botSelected === 0) {
        return "/images/Placeholder-Bot.png";
      }

      return `/images/${selectedToSymbol[this.botSelected]}-${this.botStatus}.png`;
    }
  }
}
</script>
 
<style>
#container {
  display: flex;
  flex-direction: column;
  width: 100%;
  height: 100vh;
  padding-top: 40px;
  box-sizing: border-box;
  background-color: #44D7B6;
}
 
#bot-placeholder, #you-placeholder {
  flex: 0px 2 1;
}
 
#bot-placeholder img, #you-placeholder img {
  display: block;
  width: 60%;
  height: auto;
  margin: auto;
}
 
#buttons-container {
  flex: 0px 1 1;
  display: flex;
  flex-direction: row;
}
 
#buttons-container div {
  flex: 0px 1 1;
  background-size: contain;
  background-repeat: no-repeat;
  background-position: center bottom;
}
 
#buttons-container div#btn-paper {
  background-image: url('/public/images/paper-btn.png');
}
 
#buttons-container div#btn-scissor {
  background-image: url('/public/images/scissor-btn.png');
}
 
#buttons-container div#btn-rock {
  background-image: url('/public/images/rock-btn.png');
}
</style>