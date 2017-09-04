<template>
  <div class="board" @dragover="dragover" @dragenter="dragenter" @drop="drop">
    <Card :pos="pos" @posChange="posChange"></Card>
  </div>
</template>
<script>
import Card from './Card'
  export default {
    name: 'board',
    components: {
      Card
    },
    data () {
      return {
        pos: {
          top: 30,
          left: 30,
          shadowTop: 30,
          shadowLeft: 30
        }
      }
    },
    methods: {
      dragenter (ev) {
      },
      dragover (ev) {
        ev.preventDefault()
      },
      drop (ev) {
      },
      posChange (changeVal) {
        console.log(changeVal)
        this.pos.top += changeVal.y
        this.pos.left += changeVal.x
      }
    }
  }
</script>
<style lang="css">
  .board{
    width: 100%;
    background-color:#f9f9f9;
    position: relative;
    height: 500px;
  }
</style>
