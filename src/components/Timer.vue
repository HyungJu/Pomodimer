
<template>
    <div id="timer">
      <span  id="title" v-on:click="setTitleInputSelected()" v-show="!showInput()">{{ title }}</span>
      <input v-model="title"  v-on:click="this.focus()" id="titleInput" ref="titleInput" v-on:keypress.enter="titleInputMode=false" v-show="showInput()">
      <span id="displayTimer" >{{ displayTimer }}</span>
    </div>
</template>

<script>
import Vuex from 'vuex'
import Vue from 'vue'
Vue.use(Vuex)
const audio = new Audio('/static/clock.mp3')
audio.load()
var timerInterval
export default {
  name: 'timer',
  data: function () {
    return {
      time: '',
      title: '클릭해 제목 수정',
      titleInputMode: 'false'
    }
  },
  computed: {
    displayTimer: function () {
      let minute = parseInt(this.$store.state.timerDuration / 60)
      let second = parseInt(this.$store.state.timerDuration - minute * 60)

      if (minute < 10) {
        minute = '0' + minute
      } if (second < 10) {
        second = '0' + second
      } if (second === 0) {
        second = '00'
      }

      if (!this.$store.state.timerDuration) {
        this.$store.commit('endTimer')
        this.stopTimer()
      }
      return minute + ':' + second
    }
  },
  methods: {
    showInput: function () {
      return this.titleInputMode || this.titleInputModeProps
    },
    setTitleInputSelected: function () {
      this.$refs.titleInput.focus()
    },
    stopTimer: function () {
      audio.pause()
      clearInterval(timerInterval)
      //  this.timerDuration = 0
    }
  },
  props: ['titleInputModeProps', 'timerStop'],
  mounted () {
    audio.loop = true
    audio.play().catch(() => {
    }).then(() => {
      timerInterval = setInterval(() => {
        this.$store.state.timerDuration--
      }, 1000)
    })
  },
  watch: {
    timerStop: function () {
      if (this.timerStop) {
        this.stopTimer()
      } else {
        timerInterval = setInterval(() => {
          this.$store.state.timerDuration--
        }, 1000)
      }
    }
  }
}
</script>

<style scoped>
  @import url('https://fonts.googleapis.com/css?family=Montserrat:400,700,700i');
  #timer {
    color: #FFFFFF;
    text-align: center;
  }#displayTimer{

       font-family: Montserrat;
       font-size: 5rem;
       font-weight: bold;
       margin-top: 0px;
       margin-bottom: 0px;
        font-style: italic;
     }
  #title {
    display: block;
    width: 100%;
    color: #FFFFFF;
    font-family: NanumBarunGothic;
    font-size: 2rem;
    font-weight: bold;
  }
  #titleInput {
    display: block;
    width: 100%;
    color: #FFFFFF;
    font-family: NanumBarunGothic;
    font-size: 2rem;
    font-weight: bold;
    background: transparent;
    border: none;
    text-align: center;
  }
</style>
