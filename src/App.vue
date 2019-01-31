<template>
  <div id="app">
    <transition name="slidein">
      <notification v-if='notiExists()'/>
    </transition>

    <div id="flex">

      <timer/>

      <button v-on:click="show()">토글</button>

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
      if(!this.notification){

        this.notification = 'gg'
      } else {
        this.notification = ''
      }
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



</style>
