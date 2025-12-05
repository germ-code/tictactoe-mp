<script setup lang="ts">

defineProps<{
    symbol: string
}>()

defineEmits<{
(e: 'symbolSwitch'): void
}>()


const ifCellIsClicked = defineModel('selected', {required: true})

</script>

<template>
    <div @click="ifCellIsClicked = symbol; $emit('symbolSwitch')" class="col"> <!-- When clicked, sets the var -->
        <div class="symbolInCell" v-if="ifCellIsClicked">{{ ifCellIsClicked }}</div> <!-- renders symbol after reading update from vmodel -->
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