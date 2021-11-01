<template>
  <section class="gameBoard" id="game">
    <div class="mainContainer">
        <div class="resultsContainer">
            <!-- <div class="scoreContainer">
                <p class="score">0</p>
            </div>
            <div>
                <p class="lifes">Lifes: 3</p>
            </div>
            <div>
                <p class="timerOn">Time: 60 s</p>
            </div> -->
        </div>
        <div class="canvas" id="canvas">
          <h4 :class="word" v-for="(word,index) in words"  :key="index">{{word}}</h4>
        </div>
        <div class="inputContainer">
          <form @submit.prevent="handleInput(this.wordInput)">
          <input v-model="wordInput" type="text" required class="inputText" placeholder="Enter Text" autocomplete="off">
          </form>
        </div>
    </div>
  </section>
</template>

<script>
export default {
  name: 'GameBoard',
  data: function () {
    return {
      words : ['paper'],
      wordInput: '',
      score: 0,
      lifes: 3
    }
  },
  methods: {
    handleInput: function(word) {
      console.log(word)
      if (this.words.includes(word)) {
        this.words = this.words.filter((value)=>value !== word)
      }
    }
  }
}
</script>
<style lang="scss" scoped>
.canvas {
  border-top: 5px solid red;
  border-bottom: 5px solid red;
  height: 82vh;
  width: 98%;
  margin: 0 auto;
  display: flex;
  position: relative;
  border-radius: 5px;
}
  
.gameBoard {
  overflow: hidden;
}
  
.mainContainer {
  border: 5px solid white;
  display: flex;
  flex-direction: column;
  border-radius: 5px;
}
h4 {
  color: white;
  animation: rain 7s;
  animation-fill-mode: forwards;
  position: absolute;
  animation-timing-function: linear;
  transform: rotate(40deg);
  opacity: 1;
  transition: opacity 0.2s ease-out;
  font-size: 2rem;
}

@keyframes rain {
  0% {
    background: auto;
    top: 0px;
  }
  100% {
    background: auto;
    top: 80%;
    color: red;
  }
}

.inputContainer {
  height: 8.5vh;
  display: flex;
  justify-content: center;
}
.resultsContainer {
  height: 7vh;
  display: flex;
  justify-content: space-around;
  div p {
    font-size: 2rem;
    margin: 0;
  }
}

form {
  width: 70%;
  display: flex;
}

input[type="text"] {
  height: 98%;
  width: 100%;
  font-size: 2.5rem;
  text-align: center;
  background-color: white;
  color: black;
  border: none;
  border-radius: 5px;
}
</style>
