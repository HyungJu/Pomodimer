
<template>
    <div id="timer">
      <span  id="title" v-on:click="setTitleInputSelected()" v-show="!showInput()">{{ title }}</span>
      <input v-model="title"  v-on:click="this.focus()" id="titleInput" ref="titleInput" v-on:keypress.enter="titleInputMode=false" v-show="showInput()">
      <span id="displayTimer" >{{ displayTimer }}</span>
    </div>
</template>

<script>
export default {
  name: 'timer',
  data: function () {
    return {
      time: '',
      title: '클릭해 제목 수정',
      timerDuration: 1500,
      titleInputMode: 'false'
    }
  },
  computed: {
    displayTimer: function () {
      let minute = parseInt(this.timerDuration / 60)
      let second = parseInt(this.timerDuration - minute * 60)

      if (minute < 10) {
        minute = '0' + minute
      } else if (second < 10) {
        second = '0' + second
      } else if (second === 0) {
        second = '00'
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
    }
  },
  props: ['titleInputModeProps'],
  mounted () {
    const audio = new Audio('/static/clock.mp3')

    audio.loop = true
    audio.play()
    setInterval(() => {
      this.timerDuration--
    }, 1000)
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
       font-size: 135px;
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
    font-size: 55px;
    font-weight: bold;
  }
  #titleInput {
    display: block;
    width: 100%;
    color: #FFFFFF;
    font-family: NanumBarunGothic;
    font-size: 55px;
    font-weight: bold;
    background: transparent;
    border: none;
    text-align: center;
  }
</style>
