<template>
  <div id="app">
    <h1>
      <MultiColorText text="MARIO PARTY"/>
    </h1>

    <Timer />
  </div>
</template>

<script>
import Timer from './components/Timer'
import MultiColorText from './components/MultiColorText'

export default {
  name: 'app',
  components: {
    Timer,
    MultiColorText
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1 {
  font-weight: normal;
  font-size: 50pt;
}
</style>
