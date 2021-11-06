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
            <transition v-for="(word,index) in words"  :key="index" name="rain" @after-enter="afterEnter">
              <h4 v-if="show[index]" :class="word">{{word}}</h4>
            </transition>
        </div>
        <button @click="show = !show">
          Toggle
        </button>
        <div class="inputContainer">
          <form @submit.prevent="handleInput(this.wordInput)">
          <input v-model="wordInput" type="text" required class="inputText" placeholder="Enter Text" autocomplete="off">
          </form>
        </div>
    </div>
  </section>
</template>

<script>
import randomWords from './randomWords'

export default {
  name: 'GameBoard',
  data: function () {
    return {
      words : [],
      wordInput: '',
      score: 0,
      lifes: 3,
      show: []
    }
  },
  mounted () {
    window.setInterval(() => {
      this.addWord()
      this.addListener()
    }, 1000)
  },
  methods: {
    handleInput: function(word) {
      // console.log(word)
      if (this.words.includes(word)) {
        this.words = this.words.filter((value)=>value !== word)
      }
      this.wordInput = ''
    },
    addWord: function () {
      const wordIndex = this.getRandomNumber()
      // console.log(wordIndex)
      this.words.push(randomWords[wordIndex])
      const that = this
      setTimeout(function () {
        that.show.push(true)
      }, 500)
    },
    getRandomNumber: function () {
      return Math.floor(Math.random() * randomWords.length)
    },
    addListener: function () {
      // const wordsCreated = document.querySelectorAll('h4')
      // wordsCreated.addEventListener('animationend', () => {
      //   console.log('Animation ended');
      // })
    },
    enterAnimation: function () {
      console.log('enter')
    },
    leaveAnimation: function () {
      console.log('low')
    },
    afterEnter(el) {
      console.log(el)
    },
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
  transform: rotate(40deg);
  font-size: 2rem;
  opacity: 1;
  // transition: opacity 0.2s ease-out;
  position: absolute;
}

.rain-enter-active, .rain-leave-active{
  top: 0px;
  animation: rain 7s;
}

// .rain-enter {
//   animation: rain 7s;
// }


@keyframes rain {
  0% {
    top: 0px;
  }
  100% {
    top: 80%;
    // color: red;
  }
}

@keyframes rotate {
    0% { opacity: 0; transform: scale(0) rotate(-180deg); }
    100% { opacity: 1; transform: scale(1) rotate(0deg); }
}

.rotate-enter-active {
    animation: rotate 0.2s;
}

.rotate-leave-active {
    animation: rotate 0.2s reverse;
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

.hide {
  opacity: 0;
}
</style>
