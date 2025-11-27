<script setup lang="ts">
import { ref } from 'vue';

defineProps<{
    symbol: string
}>()

const isSelected = ref(false)

// const playerAction = () => {
// }
</script>

<template>
    <div @click="isSelected = true" class="col">
        <div v-if="isSelected" class="symbolInCell">{{ $props.symbol }}</div>
    </div>
</template>


<style scoped>
.col {
    display: flex;
  border-radius: 5px;
  border: solid;
  width: 50px;
  height: 50px;
  border-color: black;
  align-items: center;
  justify-content: center;
}

.col:hover{
    cursor: pointer;
}

</style>