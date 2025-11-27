<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { Dialog } from 'primevue'
import CellComp from './components/CellComp.vue'
import PlayerSymbols from './components/PlayerSymbols.vue'
const data = ref()
onMounted(async () => {
  const res = await fetch('http://127.0.0.1:8000', {
    method: 'GET',
  })
  data.value = await res.json()
})

const playerSymbol = ref('x')
const row = 3
const col = 3

const isDialogOpen = ref(true)

</script>

<template>
  <div class="app">
    <Dialog v-model:visible="isDialogOpen" modal header="Enter Your Symbol">
      <PlayerSymbols @submit="symbolSubmmited => {playerSymbol = symbolSubmmited; isDialogOpen = false}"></PlayerSymbols>
    </Dialog>
    <div class="top-section">
      <div class="tp-menu">≡</div>
      <div class="tp-logo">Logo</div>
      <div class="tp-history">History</div>
    </div>
    <div class="board-section">
      <div v-for="i in row" :key="i" class="row">
        <CellComp v-for="j in col" :key="j" :symbol="playerSymbol"></CellComp>
      </div>
    </div>
  </div>
</template>

<style scoped>
.app {
  display: grid;
  grid-template-rows: auto 1fr;
}

.top-section {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  flex-direction: column;
  gap: 10px;
}

.tp-container {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 5px;
}

.board-section {
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  gap: 5px;
}

.row {
  display: flex;
  gap: 5px;
}
</style>
