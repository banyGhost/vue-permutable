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
  data() {
    return {
      pos: {
        top: 30,
        left: 30,
        shadowTop: 30,
        shadowLeft: 30,
        showShadow: false
      }
    }
  },
  methods: {
    dragenter(ev) {
    },
    dragover(ev) {
      ev.preventDefault()
    },
    drop(ev) {
      this.pos.showShadow = false
      this.pos.left = this.pos.shadowLeft
      this.pos.top = this.pos.shadowTop
    },
    posChange(changeVal) {
      if (window.requestAnimationFrame) {
        window.requestAnimationFrame(() => {
          this.pos.top += changeVal.y
          this.pos.left += changeVal.x
        })
      } else {
        let currTime = new Date().getTime()
        let timeToCall = Math.max(0, 16.7 - (currTime - lastTime))
        setTimeout(function() {
          this.pos.top += changeVal.y
          this.pos.left += changeVal.x
        }, timeToCall)
        lastTime = currTime + timeToCall
      }
      this.pos.showShadow = true
      this.pos.shadowLeft = 30 + Math.round(this.pos.left / 430) * 430
      this.pos.shadowTop = 30 + Math.round(this.pos.top / 320) * 320
    }
  }
}
</script>
<style lang="css">
.board {
  width: 100%;
  height: 800px;
  background-color: #f9f9f9;
  position: relative;
}
</style>
