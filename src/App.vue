<template>
  <div id="app">
    <Board></Board>
  </div>
</template>

<script>
import Board from './components/Board'
export default {
  name: 'app',
  components: {
    Board
  }
}
</script>

<style>
* {
  margin: 0px;
  padding: 0px;
}

html,
body {
  height: 100%;
  font-family: "微软雅黑";
}
</style>
