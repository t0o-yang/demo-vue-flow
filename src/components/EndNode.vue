<template>
  <NodeToolbar :is-visible="data.toolbarVisible" :position="data.toolbarPosition">
    <div class="form-label">
      上游节点列大小：<br />
      <a-input-number :value="props.colNumber" @update:value="update"></a-input-number>
    </div>
  </NodeToolbar>
  <div>{{ data.label }}</div>
  <Handle type="target" :position="Position.Left" />
</template>

<script lang="ts" setup>
import { Handle, Position, useVueFlow } from '@vue-flow/core'
import { NodeToolbar } from '@vue-flow/node-toolbar'

const props = defineProps(['id', 'data', 'colNumber'])
const emit = defineEmits(['update:colNumber'])
const { updateNodeData } = useVueFlow()

function update(val) {
  if (val) {
    // updateNodeData(props.id, )
    emit('update:colNumber', props.id, val)
  }
}
</script>

<style scoped>
.form-label {
  color: #fff;
}
</style>
