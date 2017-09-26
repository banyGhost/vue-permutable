<template>
  <div class="card">
    <div class="real-card" :style="{'left': pos.left + 'px', 'top': pos.top + 'px'}" @dragstart="dragstart" @drag="drag" v-draggable>
      <div class="card-title">标题</div>
      <div class="card-content">
        <p>我不是张随便拖动的卡片</p>
        <p>我自己知道该去到哪里</p>
        <P>一个萝卜一个坑嘛</P>
      </div>
    </div>
    <div class="shadow-card" :class="{'shadow-border': pos.shadowBorder}" :style="{'left': pos.shadowLeft + 'px', 'top': pos.shadowTop + 'px'}" v-show="pos.showShadow"></div>
  </div>
</template>
<script>
import throttle from 'lodash/throttle'
export default {
  name: 'card',
  props: {
    pos: {
      type: Object
    }
  },
  directives: {
    draggable: {
      bind: (el) => {
        el.setAttribute('draggable', true)
        el.addEventListener('selectstart', (ev) => {
          ev.preventDefault()
        })
      }
    }
  },
  data() {
    return {
      initX: 0,
      initY: 0
    }
  },
  methods: {
    dragstart(ev) {
      this.initX = ev.clientX
      this.initY = ev.clientY
    },
    drag(ev) {
      let changeVal = {
        x: ev.clientX - this.initX,
        y: ev.clientY - this.initY
      }
      throttle(() => {
        this.$emit('posChange', changeVal)
      }, 100)()
      this.initX = ev.clientX
      this.initY = ev.clientY
    }
  }
}
</script>
<style lang="css">
.real-card {
  background-color: #fff;
  width: 400px;
  height: 287px;
  position: absolute;
  border: 1px solid #e9eaec;
  box-shadow: 0 2px 4px 0 rgba(191, 200, 209, .6);
}

.shadow-card {
  width: 400px;
  height: 287px;
  position: absolute;
  border: 1px dashed #333;
}
.card-title{
  font-weight: 600;
  font-size: 18px;
  padding: 10px 15px;
  border-bottom: 2px solid #70ab8a;
}
.card-content{
  font-size: 14px;
  color: #555;
  padding: 20px 30px;
}
.card-content p{
  margin: 6px 0;
}
</style>
