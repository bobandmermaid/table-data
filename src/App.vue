<template>
  <div id='app'>
    <Data value />
  </div>
</template>

<script>
import Data from './components/Data';

export default {
  name: 'App',
  components: {
    Data
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  -ms-text-size-adjust: 100%;
  -webkit-text-size-adjust: 100%;
  font-size: 16px;
  word-spacing: 1px;
  box-sizing: border-box;
  text-align: center;
  color: #2c3e50;
  margin: 0 auto;
}

*,
*:before,
*:after {
  box-sizing: border-box;
  margin: 0;
}
</style>
