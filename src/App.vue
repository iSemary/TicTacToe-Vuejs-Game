<template>
  <div id="app">
    <h1 style="margin-bottom: 0">Tic-Tac-Toe Game</h1>
    <div>Made By Semary.</div>
    <h2 class="static">
      <span class="playerNames">X</span>
      has
      <span class="results">{{wins["X"]}}</span> wins | Match
      <span class="results">{{matches +1}}</span> |
      <span class="playerNames">O</span>
      has
      <span class="results">{{wins["O"]}}</span> wins
    </h2>
    <Grid />
    <button class="restart" @click="restart">Restart</button>
  </div>
</template>

<script>
import Grid from "./components/Grid.vue";
import EventBus from "./eventBus";
export default {
  name: 'App',
  components: {
    Grid
  },
  data(){
    return {
      matches: 0,
      wins:{
        O:0,
        X:0
      }
    }
  },
  created() {
    EventBus.$on("win", winner => this.wins[winner]++)
  },
  methods: {
    restart(){
      EventBus.$emit("clearCells");
      EventBus.$emit("resetGrid");
      this.matches++;
    }
  }
}
</script>

<style>
#app {
  font-family: 'Dosis', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
  max-width: 400px;
}
#app h1 {
  text-transform: uppercase;
  font-weight: bold;
  font-size: 3em;
}
  .restart {
    width: 100%;
    margin: 0;
    background-color: #ff5722;
    border: none;
    color: #ffffff;
    padding: 20px 0;
    border-bottom-left-radius: 50px;
    border-bottom-right-radius: 50px;
    font-size: 22px;
    font-weight: bold;
    cursor: pointer;
    outline: none;

  }
  .static {
    font-weight: 400;
  }
  .static .results {
    color: #00bcd4;
    font-weight: 800;
  }
  .static .playerNames {
    text-decoration: underline;
    color: #2c3e50;
  }
</style>
