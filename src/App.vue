<template>
  <div id="app">
    <game />
  </div>
</template>

<script>
import Game from './components/Game'

export default {
  name: 'app',
  components: { Game },
  data () {
    return {
      msg: 'debuging now'
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 4px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

.noWrap {
    display: inline-block; /* インラインブロック化 */
}
</style>
