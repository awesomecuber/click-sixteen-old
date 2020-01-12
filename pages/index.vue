<template>
  <div id="app">
    <div class="w-screen h-screen bg-blue-200 mx-auto flex flex-col items-center justify-around">
      <div class="text-4xl">
        Click Sixteen - Currrent: <b>{{ cur == 17 ? "DONE" : cur }}</b> - time {{ (time / 100).toFixed(2) }}
      </div>
      <div class="m-5 flex-1 flex flex-wrap items-stretch w-3/4 border border-gray-700">
        <div v-for="num in nums" :key="num" class="w-1/4 h-1/4">
          <button @click="cur = cur == num ? cur + 1 : cur" class="w-full h-full border-2 border-gray-700 bg-gray-400 text-6xl">
            {{ num }}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => {
    return {
      nums: [],
      cur: 1,
      time: 0,
      timer: null
    }
  },
  watch: {
    cur () {
      if (this.cur === 17) {
        clearTimeout(this.timer)
      }
    }
  },
  created () {
    const nums = []
    for (let i = 1; i <= 16; i++) {
      nums.push(i)
    }
    for (let i = nums.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1))
      const temp = nums[i]
      nums[i] = nums[j]
      nums[j] = temp
    }
    this.nums = nums

    this.timer = setInterval(() => {
      this.time += 1
    }, 10)
  }
}
</script>

<style>

</style>
