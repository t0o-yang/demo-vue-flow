<template>
  <div
    class="set-node"
    :style="{
      width: `${152 * colNumber}px`,
      height: `${42 * colNumber}px`,
      overflowY: 'auto',
      gridTemplateColumns: '1fr '.repeat(colNumber)
    }"
  >
    <div
      class="set-node-childrenNode"
      v-for="node in data.children"
      @mouseover="(e) => mouseover(node, e)"
    >
      {{ node.data.label }}
    </div>
  </div>
  <Handle id="a" type="target" :position="Position.Left" />
  <Handle id="b" type="source" :position="Position.Right" />
</template>

<script lang="ts" setup>
import { ref } from 'vue'
import { Handle, Position, useVueFlow } from '@vue-flow/core'
import type { Node } from '@vue-flow/core'

const props = defineProps({
  id: {
    type: String,
    required: true
  },
  data: {
    type: Object,
    required: true
  },
  colNumber: {
    type: Number
  }
})
const emits = defineEmits(['hover'])
console.log('🚀 ~ props:===》\n', props.id, props.colNumber)

function mouseover(node: Node, e) {
  node.position = {
    x: e.x - 354,
    y: e.y - 80
  }
  console.log('🚀 ~ mouseover ~ node:===》\n', node)
  console.log('🚀 ~ mouseover ~ e:===》\n', e)
}
</script>

<style scoped>
.set-node {
  padding: 5px;
  border: 1px dashed black;
  border-spacing: 15px;
  border-radius: 3px;
  display: grid;
  grid-gap: 5px 5px;
}
.set-node-childrenNode {
  /* width: 152px; */
  /* height: 21px; */
  border: 1px solid;
  border-radius: 3px;
}
.set-node-childrenNode:hover {
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}
</style>
