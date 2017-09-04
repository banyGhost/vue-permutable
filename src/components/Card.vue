<template>
  <div class="card">
    <div class="real-card" :style="{'left': pos.left + 'px', 'top': pos.top + 'px'}" @dragstart="dragstart" @drag="drag" v-draggable>
      <slot name="title"></slot>
      <slot name="content"></slot>
    </div>
    <div class="shadow-card" :style="{'left': pos.shadowLeft + 'px', 'top': pos.shadowTop + 'px'}" v-show="showShadow"></div>
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
    data () {
      return {
        showShadow: false,
        initX: 0,
        initY: 0
      }
    },
    methods: {
      initPos () {

      },
      dragstart (ev) {
        this.initX = ev.clientX
        this.initY = ev.clientY
      },
      drag (ev) {
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
  }
  .shadow-card {
    width: 400px;
    height: 287px;
    position: absolute;
    border:1px dashed #333;
  }
</style>
