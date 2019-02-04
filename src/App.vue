<template>
  <div id="app" v-on:click="titleInputMode = true">
    <transition name="slidein">
      <notification v-bind:message='notification' v-if='notiExists()'/>
    </transition>

    <div id="flex">

      <timer titleInputModeProps="titleInputMode"/>
      <!--
      <button v-on:click="show()">토글</button>
      <button v-on:click="change()">내용 변경</button>
      -->
      <div id="stopBox">
        <i id="stop" v-on:click="stop()" class="fas fa-stop"></i>
      </div>

      <ul>
        <li v-for="lemon of lemons" :key="lemon">
          <i class="fas fa-lemon"></i> {{lemon}}
        </li>
      </ul>
    </div>

  </div>

</template>

<script>

import Timer from './components/Timer'
import Notification from './components/Notification'
export default {
  components: {Notification, Timer},
  data: function () {
    return {
      msg: '안농',
      notification: '',
      lemons: [0, 1, 2, 3, 4, 5],
      titleInputMode: false
    }
  },
  methods: {
    show: function () {
      if (!this.notification) {
        this.notification = 'gg'
      } else {
        this.notification = ''
      }
    },
    change: function () {
      this.notification = 'gg1'
    },
    notiExists: function () {
      return this.notification
    },
    stop: function () {
      Timer.methods.stopTimer()
    }

  }
}
</script>

<style>
  body{
    margin: 0;
    padding: 0;
    background-color: #212121;
  }
  #flex{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;
    text-align: center;
    flex-direction: column;
  }#notificationArea{
     display: flex;
     justify-content: center;
   }
  #stopBox {
    height: 30px;
    width: 30px;
    padding:20px;
    border: 1px solid white;
    border-radius: 50px;
    margin-top:40px;
  }
  #stop{

    font-size: 30px;

    color: white;
         }
ul{
  display: flex;
  list-style-type: none;
  color:white;
  margin: 0;
  padding: 0;

}li{
    padding: 5px;
    font-size: 30px;

   left: 0;
   bottom: 0;
   width: 100%;
   color: white;
   text-align: center;
 }
</style>
