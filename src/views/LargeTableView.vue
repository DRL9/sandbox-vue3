<script setup>
import { onUpdated, ref } from 'vue'

const rowCount = ref(1000)
const colCount = ref(50)
const data = ref([])
const costTime = ref(0)
let startTime = Date.now()
const handleStartRender = () => {
  data.value = Array.from({ length: rowCount.value }).map((_, idx) => ({
    id: idx + '-' + Date.now(),
    cols: Array.from({ length: colCount.value }).map(
      (_, colIdx) => `${idx}-${colIdx}-${Date.now()}`
    )
  }))
  startTime = Date.now()
}
window.onscroll = () => {
  handleStartRender()
  console.time('render')
  requestAnimationFrame(() => {
    console.timeEnd('render')
  })
}
</script>

<template>
  <div>
    <div>cost time: {{ costTime }}</div>
    <div>row: <input v-model="rowCount" /></div>
    <div>col: <input v-model="colCount" /></div>
    <div>
      <button @click="handleStartRender">开始渲染</button>
    </div>
    <div class="table-wrap">
      <table :key="rowCount + '-' + colCount">
        <tr v-for="row in data" :key="row.id">
          <td v-for="col in row.cols" :key="col">{{ col }}</td>
        </tr>
      </table>
    </div>
  </div>
</template>

<style scoped>
.table-wrap {
  width: 100vw;
}
table {
  border: 1px solid #ccc;
  border-collapse: collapse;
}
td {
  border: 1px solid #ccc;
}
</style>
