<template>
  <div class="set-node"></div>
  <Handle id="a" type="target" :position="Position.Left" />
  <Handle id="b" type="source" :position="Position.Right" />
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { Handle, Position, useVueFlow } from '@vue-flow/core'

const props = defineProps({
  id: {
    type: String,
    required: true
  },
  data: {
    type: Object,
    required: true
  }
})
</script>

<style scoped>
.set-node {
  border: 1px dotted;
}
</style>
