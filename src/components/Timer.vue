<template>
  <div class="timer" v-bind:class="[ timerActive ? 'timer-active': 'timer-stopped' ]">
    <div class="timer-form">
      <input type="text" v-model="time" />
      <button class="no-shadow-thin" @click="start">Start</button>
    </div>
    <div class="current-time">
      <h1 class="callout" v-if="callout">{{callout}}</h1>
      <h1 v-if="currentTime">{{currentTime}}</h1>
    </div>
  </div>
</template>

<script>
import StartWav from '../assets/audio/start.wav'
import FinishWav from '../assets/audio/finish.wav'

export default {
  name: 'Timer',
  methods: {
    start
  },
  data () {
    return {
      time: 60,
      timerActive: false,
      currentTime: null,
      interval: null,
      callout: null
    }
  }
}

const startAudio = new Audio(StartWav)
const finishAudio = new Audio(FinishWav)
const START = 'START'
const FINISH = 'FINISH'

function start() {
  startAudio.play()
  this.timerActive = true
  this.callout = START

  setTimeout((instance) => {
    this.callout = null
    instance.currentTime = Number(instance.time)
    incrementTime.call(instance)
  }, 1000, this)
}

function stop() {
  finishAudio.play()
  this.callout = FINISH
  this.currentTime = null
  clearInterval(this.interval)

  setTimeout((instance) => {
    instance.timerActive = false
    this.callout = null
  }, 1000, this)
}

function incrementTime() {
  this.interval = setInterval((instance) => {
    instance.currentTime--

    if (!instance.currentTime) {
      stop.call(instance)
    }
  }, 1000, this)
}
</script>

<style scoped>
.timer {
  text-align: center;
  -webkit-text-stroke-width: 3px;
  -webkit-text-stroke-color: #fffdfd;
  text-shadow: none
}

.timer-active .timer-form {
  display: none;
}

.current-time h1 {
  font-size: 75pt;
  color: orange;
}

.timer-stopped .current-time {
  display: none;
}

h1 {
  font-weight: normal;
  font-size: 40pt;
}

input {
  border: orange solid 6px;
  background: #ffec80;
  font-size: 50pt;
  width: 20vw;
  text-align: center;
}

button {
  display: block;
  margin: 35px  auto;
  background: transparent;
  font-size: 35pt
}

.current-time  h1.callout {
  font-size: 65pt
}
</style>
