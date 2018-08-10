<template>
  <div id="app">
    <button @click="onClickBtn">点我出字幕</button>
    <transition
      @before-enter="beforeEnter"
      @enter="enter"
      :css="false">
      <span id="fly-span" v-if="show">{{txt}}</span>
    </transition>
  </div>
</template>

<script>
import {TweenLite, Ease} from "gsap/TweenMax"

export default {
  name: 'app',
  data () {
    return {
      show: false,
      txt: ''
    }
  },
  methods: {
    onClickBtn () {
      this.show = true
      this.txt = (Math.random() * 10000).toString()
    },
    beforeEnter(el) {
      TweenLite.set(el, {left: '100%'})
    },
    enter(el) {
      TweenLite.to(el, .5, {
        left: '50%',
        ease: Ease.easeIn,
        onComplete: () => {
          TweenLite.to(el, 1.3, {
            left: '45%',
            ease: Ease.easeOut,
            onComplete: () => {
              TweenLite.to(el, .2, {
                left: '-200px',
                ease: Ease.easeOut,
                onComplete: () => {
                  this.show = false
                }
              },)
            }
          },)
        }
      })
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

#fly-span {
  width: 200px;
  height: 60px;
  background-color: #F00;
  color: #FFF;
  font-size: 20px;
  position: absolute;
}
</style>
