<template>
  <div class="hello">
    <Square v-for="(item, idx) in squares" :key="idx" :value="item" :idx="idx" :clickButton="handleClick" />
  </div>
</template>

<script>
import { reactive, toRefs } from '@vue/composition-api'
import Square from '@/components/Square.vue'

export default {
  name: 'TicTacToe',
  setup () {
    const state = reactive({
      currType: 1,
      squares: Array(9).fill(0),
      finish: false
    })

    const list = [
      [0, 1, 2],
      [3, 4, 5],
      [6, 7, 8],
      [0, 3, 6],
      [1, 4, 7],
      [2, 5, 8],
      [0, 4, 8],
      [2, 4, 6]
    ]

    const computer = () => {
      let _squares = state.squares.map((item, idx) => {
        if (item === 0) {
          return idx
        }
      })
      _squares = _squares.filter(item => {
        return item !== undefined
      })
      if (_squares.length <= 1 && state.currType === -1) {
        return
      }
      const random = Math.floor(Math.random() * _squares.length)
      const number = _squares[random]
      state.squares.splice(number, 1, state.currType)
      state.currType = -state.currType
    }

    const handleClick = idx => {
      if (state.finish) {
        return
      }
      state.squares.map((item, _idx) => {
        if (idx === _idx) {
          state.squares.splice(idx, 1, state.currType)
        }
      })
      state.currType = -state.currType
      !state.finish && isFinished()
      !state.finish && computer()
      !state.finish && isFinished()
    }

    const reset = type => {
      state.finish = false
      state.squares = Array(9).fill(0)
      state.currType = type === 0 ? 1 : type
      if (state.currType === -1) {
        state.currType = -state.currType
        computer()
      }
    }

    const isFinished = () => {
      for (const item of list) {
        const [x, y, z] = item
        const result = state.squares[x] + state.squares[y] + state.squares[z]
        if (Math.abs(result) === 3) {
          setTimeout(() => {
            result === 3 ? alert('O赢了！') : alert('X赢了！')
          })
          state.finish = true
          break
        }
      }
    }

    return {
      ...toRefs(state),
      handleClick,
      reset,
      isFinished
    }
  },
  components: {
    Square
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="less">
.hello {
  width: 150px;
  height: 150px;
  border: 1px solid #ccc;
  display: flex;
  flex-flow: row wrap;
  align-items: flex-start;
  transform: translateY(200px) scale(0.99999);
}
</style>
