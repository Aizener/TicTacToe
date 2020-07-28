<template>
  <div class="square">
    <button @click="handleClick">
      {{ show }}
    </button>
  </div>
</template>

<script>
import { reactive, toRefs, computed } from '@vue/composition-api'

export default {
  name: 'Square',
  props: ['idx', 'value', 'clickButton'],
  setup (props) {
    const state = reactive({
      showType: ['X', null, 'O'],
      show: computed(() => {
        return state.showType[props.value + 1]
      })
    })
    const handleClick = () => {
      if (props.value) {
        return
      }
      props.clickButton(props.idx)
      state.isClick = true
    }

    return {
      ...toRefs(state),
      handleClick
    }
  }
}
</script>

<style lang="less" scoped>
button {
  width: 50px;
  height: 50px;
  outline: none;
  border: 1px solid #ccc;
  box-sizing: border-box;
  padding: 0;
  background: #fff;
  vertical-align: bottom;
  color: gray;
  font-size: 25px;
}
</style>
