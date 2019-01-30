<template>
  <div id="app">
    <transition name="slidein">
      <notification v-if='notiExists()'/>
    </transition>
    <div id="flex">

      <button v-on:click="show()">보기</button>
      <timer/>
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
      notification: ''
    }
  },
  methods: {
    show: function () {
      this.notification = 'gg'
    },
    notiExists: function () {
      return this.notification
    }

  }
}
</script>

<style>
  body{
    margin: 0;
    padding: 0;
    background-color: #E8554D;
  }
  #flex{
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    width: 100vw;

  }#notificationArea{
     display: flex;
     justify-content: center;
   }
  .slidein-enter-active {
    transition: all .3s ease;
  }
  .slidein-enter
    /* .slide-fade-leave-active below version 2.1.8 */ {
    transform: translatey(-10px);
    opacity: 0;
  }.sidein-enter-active{
    transition: 1s;
    left: 0;
  }
</style>
