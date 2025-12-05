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

const row = 3
const col = 3

// place holder incase players dont want to enter their own symbol
const playerOneSymbol = ref('X') 
const playerTwoSymbol = ref('O')

// place holder to be updated for switching function
const currentTurn = ref('X')

const gameState = ref([
  [null,null,null],
  [null,null,null],
  [null,null,null]
  ]
)

// Switch CurrentTurn var function
function switchCurrentTurn (){
  if (currentTurn.value == playerOneSymbol.value) {
    currentTurn.value = playerTwoSymbol.value
  } else {
    currentTurn.value = playerOneSymbol.value
  }
  console.log('switchCurrentTurn called!')
  console.log('currentTurn', currentTurn.value)
  console.log('playerOneSymbol', playerOneSymbol.value)
} 


const winCondtion = null
const isDialogOpen = ref(true)

</script>

<template>
  <div class="app">
    <Dialog v-model:visible="isDialogOpen" modal header="Enter Your Symbol">
      <PlayerSymbols @submit="playerSymbolData => {currentTurn = playerSymbolData; playerOneSymbol = playerSymbolData; isDialogOpen = false}"></PlayerSymbols>
    </Dialog>
    <div class="top-section">
      <div class="tp-menu">≡</div>
      <div class="tp-logo">Logo</div>
      <div class="tp-history">History</div>
    </div>
    <div class="board-section" v-if="gameState">
      <div v-for="i in row" :key="i" class="row">
        <CellComp v-model:selected="gameState[i-1][j-1]" v-for="j in col" :key="j" :symbol="currentTurn" @symbolSwitch="switchCurrentTurn"></CellComp>
      </div>
      {{ gameState }}
      <div></div>
      {{ playerTwoSymbol }}
      {{ playerOneSymbol }}
      <div></div>
      {{ currentTurn }}
      <div>
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
  flex-direction: row;
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
