<template>
  <div id="app">
    <TicTacToe ref="ticTacToe" />
    <div>
      <button @click="reset(1)">执先</button>
      <button @click="reset(-1)">执后</button>
      <button @click="reset(0)">重置</button>
    </div>
  </div>
</template>

<script>
import TicTacToe from '@/components/TicTacToe.vue'

export default {
  name: 'App',
  setup (props, ctx) {
    const reset = type => {
      ctx.refs.ticTacToe.reset(type)
    }
    return {
      reset
    }
  },
  components: {
    TicTacToe
  }
}
</script>

<style lang="less" scoped>
#app {
  display: flex;
  flex-direction: column;
  align-items: center;
  button {
    margin: 0 5px;
    outline: none;
    border: 1px solid #ccc;
    color: gray;
    padding: 5px 10px;
  }
}
</style>
