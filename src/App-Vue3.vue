<template>
  <div id="app">
    <div>
      <!-- {{ count }} -->
      <!-- {{ state.count }} -->
      <!-- {{ count }} -->
      <!-- {{ count }} ,  -->
      <!-- {{ double }} -->
      <div>{{ count }}</div>
      <button @click="add">count累加</button>

    </div>
  </div>
</template>

<script>

import { reactive, ref, toRefs, toRef, computed, watchEffect } from '@vue/composition-api'

export default {
  name: 'App',
  setup () { //Vue3.0的入口函数，在beforeCreate之前触发

    // 不具备响应式
    // const state = reactive({
    //   count: 0
    // })
    // return state

    // 具备响应式
    // const state = reactive({
    //   count: 0
    // })
    // setInterval(() => {
    //   state.count++
    // }, 1000)
    // return {
    //   state
    // }

    // 使用ref
    // const count = ref(0)
    // setInterval(() => {
    //   count.value++
    // }, 1000)
    // return {
    //   count
    // }

    // ---------------------------------------------------------------------
    // const count = ref(0)
    // const state = reactive({
    //   count
    // })
    // setInterval(() => {
    //   state.count++
    // }, 1000)
    // return {
    //   count
    // }

    // const state = reactive({
    //   count: 0
    // })
    // const { count } = toRefs(state) // 把普通的数据转成ref()方法对应的响应式数据
    // setInterval(() => {
    //   state.count++
    // }, 1000)
    // return {
    //   count
    // }

    // const state = reactive({
    //   count: 0
    // })
    // setInterval(() => {
    //   state.count++
    // }, 1000)
    // return toRefs(state)

    // const state = reactive({
    //   count: 0
    // })
    // const count = toRef(state, 'count')
    // setInterval(() => {
    //   state.count++
    // }, 1000)
    // return {
    //   count
    // }

    // ---------------------------------------------------------------------

    // const count = ref(0)
    // const double = computed(() => count.value * 2)
    // setInterval(() => {
    //   count.value++
    // }, 1000)
    // return {
    //   count,
    //   double
    // }

    // const state = reactive({
    //   count: 1,
    //   double: computed(() => state.count * 2)
    // })
    // setTimeout(() => {
    //   state.count++
    // }, 1000)
    // return toRefs(state)

    // ---------------------------------------------------------------
    // const count = ref(0)

    // const add = () => {
    //   return count.value++
    // }

    // return {
    //   count,
    //   add
    // }

    // ---------------------------------------------------
    const count = ref(0)

    const add = () => {
      count.value++
      if (count.value == 5) {
        stop()
      }
    }

    const stop = watchEffect(() => {
      console.log(count.value)
    })

    return {
      count,
      add
    }
  }
}
</script>

<style>
</style>
