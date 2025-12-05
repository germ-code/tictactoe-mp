<script setup lang="ts">
import InputText from 'primevue/inputtext'
import { Button } from 'primevue'
import { ref } from 'vue'

const playerSymbol = ref()

defineEmits<{
  (e: 'submit',  playerSymbolData:string): void
}>()
</script>

<template>
  <div style="display: flex; flex-direction: column; gap: 1rem">
    <InputText type="text" v-model="playerSymbol" maxlength="1" minlength="1"/>
    <Button :disabled="!playerSymbol" label="Done" @click="$emit('submit', playerSymbol)"></Button>
  </div>
</template>

<style scoped>
</style>
