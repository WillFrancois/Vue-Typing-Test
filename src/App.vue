<template>
  <div id="app">
    <h1 v-if="timeLeft >= 0">{{ timeLeft }}</h1>
    <WordBox
      :currentWord = "wordToType"
    />
    <Input
      :currentWord = "wordToType"
      :newWord = "newWord"
      :runTimer = "runTimer"
      v-if="timeLeft >= 0"
    />
    <button v-if="timeLeft < 0" @click="refreshPage()">Try Again?</button>
    <p>A Typing Test, Created by William Francois</p>
  </div>
</template>

<script>
import WordBox from './components/WordBox.vue'
import Input from './components/Input.vue'
import Words from './assets/words.json'

export default {
  name: 'App',
  components: {
    WordBox,
    Input
  },
  data() {
      return {
          wordToType: "",
          wordListLocal: Words,
          wordList: [],
          wordIndex: 0,
          wordsCompleted: 0,
          testStarted: false,
          timeLeft: 60,
          intervalStop: 0
      }
  },
  methods:{
    newWord(value){
      if( this.wordToType.toUpperCase() === value.toUpperCase() ){
        this.wordsCompleted++
        this.wordIndex++
        this.wordToType = this.wordList[this.wordIndex]
        document.getElementById("user-input").value = ""
      }
    },
    runTimer(){
      if(!this.testStarted){ 
        this.intervalStop = setInterval(() => {this.timeLeft--; if(this.timeLeft < 0){clearInterval(this.intervalStop); this.wordToType = "You got " + this.wordsCompleted + " words right!";} 
          }, 1000)
        this.testStarted = true;
      }
    },
    refreshPage(){
      location.reload(true)
    }
  },
  mounted: function(){
    for(var i = 0; i < 500; i++){
      this.wordList.push(this.wordListLocal[Math.floor(Math.random()*178187)])
      this.wordToType = this.wordList[this.wordIndex]
    }
  }
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  overflow: hidden;
}
h1{
  font-size: 4vh;
}
button{
  background-color:white;
  border: solid 1px;
  height: 30vh;
  width: 40vw;
  font-size: 5vh;
}
</style>
