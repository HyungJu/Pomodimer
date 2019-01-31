
<template>
    <div id="timer">
      <span id="title">형주단어장 만들기</span>
      <span id="displayTimer">{{ displayTimer }}</span>
    </div>
</template>

<script>
const numeral = require('numeral')
export default {
  name: 'timer',
  data: function () {
    return {
      time: '',
      timerDuration: 1500
    }
  },
  computed: {
    displayTimer: function () {
      return numeral(this.timerDuration).format('00:00')
    }
  },
  mounted () {
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
</style>
