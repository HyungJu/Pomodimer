<template>
  <div id="app" v-on:click="titleInputMode = true">
    <transition name="slidein">
      <notification v-bind:message='notification' v-if='notiExists()'/>
    </transition>

    <div id="flex">

      <timer :timerStop="timerStop" :titleInputModeProps="titleInputMode"/>
      <!--
      <button v-on:click="show()">토글</button>
      <button v-on:click="change()">내용 변경</button>
      -->
      <div id="stopBox">
        <i id="stop" v-on:click="stop()" class="fas fa-stop"></i>
      </div>

    </div>
    <ul>
      <li v-for="lemon of lemons" :key="lemon">
        <i class="fas fa-lemon"></i>
      </li>
    </ul>
  </div>

</template>

<script>

import Timer from './components/Timer'
import Notification from './components/Notification'
import Vuex from 'vuex'
import Vue from 'vue'
Vue.use(Vuex)
export const store = new Vuex.Store({
  state: {
    timerEnded: false
  },
  mutations: {
    endTimer (state) {
      state.timerEnded = true
    },
    startTimer (state) {
      state.timerEnded = false
    }
  }
})
export default {
  components: {Notification, Timer},
  store,
  data: function () {
    return {
      msg: '안농',
      notification: '',
      lemons: [],
      titleInputMode: false,
      timerStop: false,
      vuexStore: store
    }
  },
  computed: {
    timerEnded: function () {
      return store.state.timerEnded
    }
  },
  watch: {
    timerEnded: function () {
      this.lemons.push('gg')
    }
  },
  methods: {
    show: function () {
      if (!this.notification) {
        this.notification = '형주타이머입니당. 꺄르르'
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
      this.timerStop = true
    }

  },
  mounted: function () {
    this.$on('timerEnd', (title) => {
      console.log(title)
      this.lemons.push(title)
    })
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
    height: 1.3rem;
    width: 1.3rem;
    padding:1rem;
    border: 1px solid white;
    border-radius: 50px;
    margin-top:40px;
  }
  #stop{

    font-size: 1.3rem;

    color: white;
         }
ul{
  position: absolute;
  list-style-type: none;
  color:white;
  padding-left: 0;
  left: 50%; /* position the left edge of the element at the middle of the parent */
  bottom: 1rem;
  transform: translateX(-50%);
  padding-right: 0.5rem;
}li{
    padding-left: 0.5rem;
    font-size: 1.5rem;

   float: left;

 }

  .slidein-enter{

    transform: translateY(-110%);
  }
  .slidein-enter-active{
    transition: 1s;
  }
  .slidein-leave-active{
    transition: 2s;
  }
  .slidein-leave-to{

    transform: translateY(-300%);
  }
</style>
