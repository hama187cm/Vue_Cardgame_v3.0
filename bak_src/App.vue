<template>
  <div id="app">
    <link
      rel="stylesheet"
      href="https://fonts.googleapis.com/css?family=Roboto:300,400,500,700,400italic|Material+Icons"
    >
    <md-button class="md-raised md-primary" @click="drawCard">dialog</md-button>
    <md-button class="md-raised md-primary" @click="deleteCard">
      <i class="material-icons dialog__close">clear</i>
    </md-button>
    <div v-for="(item, index) in users">
      <transition>
        <div class="dialog" v-drag v-if="isShow" :style="dialogStyle">
          <div class="dialog__header">
            <span>{{index}} - {{ item.id }}</span>
          </div>
        </div>
      </transition>
    </div>
  </div>
</template>

<script>
import drag from "@branu-jp/v-drag";
import Game from './components/Game'

export default {
  name: "App",
  data() {
    return {
      isShow: false,
      index: 0,
      dialogStyle: {
        top: 50 + "px",
        left: 50 + "px"
      },
      users: [
        {
          id: 1,
          name: "♠",
          num: "1"
        },
        {
          id: 2,
          name: "♥",
          num: "2"
        }
      ]
    };
  },
  methods: {
    dialogToggle: function() {
      this.isShow = !this.isShow;
    },
    drawCard: function() {
      this.isShow = true;
      this.index++;
      console.log("index=" + this.index);
    },
    deleteCard: function() {
      this.isShow = false;
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 8px;
}
.dialog {
  position: absolute;
  width: 50px;
  box-shadow: 4px 4px 4px rgba(0, 0, 0, 0.2);
  background-color: #fff;
  z-index: 99999;
  border-radius: 2px;
  border: 1px solid #f0f0f0;
  cursor: move;
  &__header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    background-color: #f0f0f0;
    padding: 8px 8px;
  }
  &__close {
    cursor: pointer;
  }
}
</style>
