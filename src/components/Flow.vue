<script setup lang="ts">
import { ref, onMounted, nextTick } from 'vue'
import type { Node, Edge } from '@vue-flow/core'
import { Position, VueFlow } from '@vue-flow/core'
import EndNode from './EndNode.vue'
import SetNode from './SetNode.vue'
import { reactive } from 'vue'

// these components are only shown as examples of how to use a custom node or edge
// you can find many examples of how to create these custom components in the examples page of the docs
// import SpecialNode from './components/SpecialNode.vue'
// import SpecialEdge from './components/SpecialEdge.vue'

const props = defineProps({
  canvasSize: {
    type: Object
  }
})
const res = {
  linksArray: [
    {
      source: 0,
      target: 1
    },
    {
      source: 1,
      target: 22
    },
    {
      source: 0,
      target: 2
    },
    {
      source: 2,
      target: 22
    },
    {
      source: 0,
      target: 3
    },
    {
      source: 3,
      target: 23
    },
    {
      source: 0,
      target: 4
    },
    {
      source: 4,
      target: 23
    },
    {
      source: 0,
      target: 5
    },
    {
      source: 5,
      target: 23
    },
    {
      source: 0,
      target: 6
    },
    {
      source: 6,
      target: 21
    },
    {
      source: 0,
      target: 7
    },
    {
      source: 7,
      target: 21
    },
    {
      source: 0,
      target: 8
    },
    {
      source: 8,
      target: 21
    },
    {
      source: 0,
      target: 9
    },
    {
      source: 9,
      target: 21
    },
    {
      source: 0,
      target: 10
    },
    {
      source: 10,
      target: 21
    },
    {
      source: 0,
      target: 11
    },
    {
      source: 11,
      target: 21
    },
    {
      source: 0,
      target: 12
    },
    {
      source: 12,
      target: 21
    },
    {
      source: 0,
      target: 13
    },
    {
      source: 13,
      target: 21
    },
    {
      source: 0,
      target: 14
    },
    {
      source: 14,
      target: 21
    },
    {
      source: 0,
      target: 15
    },
    {
      source: 15,
      target: 21
    },
    {
      source: 0,
      target: 16
    },
    {
      source: 16,
      target: 21
    },
    {
      source: 0,
      target: 17
    },
    {
      source: 17,
      target: 21
    },
    {
      source: 0,
      target: 18
    },
    {
      source: 18,
      target: 22
    },
    {
      source: 0,
      target: 19
    },
    {
      source: 19,
      target: 20
    }
  ],
  sourceSystemArray: [
    {
      code: 'alipay',
      title: '支付宝系统'
    }
  ],
  sceneArray: [
    {
      code: 'AlipayChargeQuery',
      title: '支付宝收费项目查询',
      type: 'actionNode'
    },
    {
      code: 'AlipayPay',
      title: '支付宝线上支付',
      type: 'actionNode'
    },
    {
      code: 'HIP.NumSourceInfo.Query',
      title: '号源排班信息查询',
      type: 'actionNode'
    },
    {
      code: 'HIP.OutreservationStatusInfo',
      title: '门诊预约状态信息新增、更新',
      type: 'actionNode'
    },
    {
      code: 'HIP.OutreservationStatusInfo.Query',
      title: '门诊预约状态信息查询',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_adv_detail',
      title: '费用查看（医嘱详情）',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_adv_list',
      title: '费用查看(医嘱列表)',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_fs_detail',
      title: '检查报告查询（获取放射报告详情）-心电接口',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_fs_list',
      title: '检查报告查询（获取放射报告列表）-心电接口',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_regist_detail',
      title: '就诊信息查看（挂号详情）',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_regist_list',
      title: '就诊信息查看（挂号列表）',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_techrpt_detail',
      title: '检验报告查询（获取检验报告详情）',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_get_techrpt_list',
      title: '检验报告查询（获取检验报告列表）',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_mzzj_get_techrpt_detail',
      title: '检查报告查询（获取放射报告详情-新）-放射、超声接口',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_mzzj_get_techrpt_list',
      title: '检查报告查询（获取放射报告列表-新）-放射、超声接口',
      type: 'actionNode'
    },
    {
      code: 'HIP.platform_pay',
      title: '在线交费(医嘱付费-自费患者)',
      type: 'actionNode'
    },
    {
      code: 'HIP.SE04',
      title: '在线交费(医保支付查询-医保患者)',
      type: 'actionNode'
    },
    {
      code: 'OutPatientInfoAdd',
      title: '门诊挂号信息新增服务',
      type: 'actionNode'
    },
    {
      code: 'PatientInfoRegister',
      title: '个人信息注册服务',
      type: 'actionNode'
    }
  ],
  targetSystemArray: [
    {
      code: 'EMPI',
      title: '患者主索引'
    },
    {
      code: 'HIS',
      title: '医院信息管理系统'
    },
    {
      code: 'HSB',
      title: 'HSB'
    },
    {
      code: 'YY',
      title: '门诊预约管理系统'
    }
  ]
}
const flowData = ref({})
if (res.sourceSystemArray && res.sceneArray && res.targetSystemArray && res.linksArray) {
  let obj = {
    nodes: [
      res.sourceSystemArray.map((node, j) => ({
        id: `0-${j}`,
        levelI: 0,
        levelJ: j,
        ...node
      })),
      res.sceneArray.map((node, j) => ({
        id: `1-${j}`,
        levelI: 1,
        levelJ: j,
        ...node
      })),
      res.targetSystemArray.map((node, j) => ({
        id: `2-${j}`,
        levelI: 2,
        levelJ: j,
        ...node
      }))
    ], // nodes 二维数组，[i][j], i 表示所在的层级
    links: res.linksArray
  }
  flowData.value = obj
}

const rawData = JSON.parse(JSON.stringify(flowData.value))
const NodeSize = { width: 152, height: 42 }
console.log('🚀 ~ rawData:===》\n', rawData)

const nodes = ref<Node[]>([])
// 包含连线信息的节点
interface NodeWithRelate {
  [id: string]: {
    pre: string[]
    next: string[]
  }
}
const nodeWithRelate: NodeWithRelate = {}

const padding = {
  left: 10,
  right: 10
}

const columnItems: {
  [id: string]: number
} = reactive({
  '2-0': 3
})

// these are our edges
const edges = ref<Edge[]>([])

function setNodes() {
  nodes.value = flowData.value.nodes.flatMap((level, i, array) => {
    const nodes = level
    const count = level.length // 当前层的节点数量
    const countHeight = count * NodeSize.height // 当前层节点总高度
    const levelWidth = array.length * NodeSize.width // 所有层的最宽节点的总宽度
    const Gap = {
      height: (props.canvasSize.height - countHeight) / (count + 1),
      width:
        (props.canvasSize.width - levelWidth - padding.left - padding.right) / (array.length - 1)
    } // 所有 margin
    // 垂直方向使用 space-around 的布局逻辑
    // 水平方向使用 space-between 的布局逻辑

    const flowNodes = []
    let X = 0
    const nodeProps = {
      type: undefined
    }
    if (i == 0) {
      // 第一层
      X = 0 + padding.left
      nodeProps.type = 'input'
    } else if (i == array.length - 1) {
      // 最后一层
      X = props.canvasSize.width - NodeSize.width - padding.right
      nodeProps.type = 'end'
      nodeProps['toolbarPosition'] = Position.Top
    } else {
      X = i * (NodeSize.width + Gap.width) + padding.left
    }
    let nodeHeightCount = 0 // 累计的节点高度
    for (let j = 0; j < nodes.length; j++) {
      const gap = Gap.height * (j + 1) + nodeHeightCount
      nodeHeightCount += NodeSize.height
      const node = nodes[j]
      if (node.type == 'set') {
        // console.log('集合节点内容：', node)
      }
      flowNodes.push({
        id: node.id,
        position: { x: X, y: gap },
        data: { label: node.title, ...node },
        sourcePosition: 'right',
        targetPosition: 'left',
        ...nodeProps,
        type: nodeProps.type || node.type
      })
    }
    return flowNodes
  })
}

// 初始化边，将索引转变为 node.id
function initEdges() {
  edges.value = flowData.value.links.map((ele, i) => {
    ele.source = rawData.nodes.flat()[ele.source].id
    ele.target = rawData.nodes.flat()[ele.target].id
    return {
      id: i,
      ...ele
    }
  })
}

function changeLayout(id, val) {
  columnItems[id] = val
  if (nodes.value?.find((node) => node.id == `set:${id}`)) {
    // console.log('节点已经存在', id, val)
  } else {
    // findRelatedNode(id)
    updateRelatedNode(id)
  }
}

function findRelatedNode(rootId) {
  // console.log('源数据', JSON.parse(JSON.stringify(flowData.value)))
  const relatedEdges = edges.value.filter((edge) => edge.target == rootId)
  const relatedNodes = relatedEdges.map((edge) => {
    return nodes.value.find((node) => node.id == edge.source)
  })
  // console.log('🚀 ~ findRelatedNode ~ relatedNodes:===》\n', relatedEdges, relatedNodes)
  // relatedEdges.forEach((edge) => {
  //   if (edge != null) {
  //     const { source, target } = edge
  //     const i = flowData.value.links.findIndex(
  //       (link) => link.source == source && link.target == target
  //     )
  //     i != -1 && flowData.value.links.splice(i, 1)
  //   }
  // })
  relatedNodes.forEach((node) => {
    if (node != null) {
      const i = node.id.split('-')[0]
      const { code, title } = node.data
      const j = flowData.value.nodes[i].findIndex(
        (node) => node.code == code && node.title == title
      )
      j != -1 && flowData.value.nodes[i].splice(j, 1)
    }
  })
  // console.log('源数据', flowData.value)

  const preLevel = rootId.split('-')[0] - 1
  if (preLevel < 0) return
  flowData.value.nodes[preLevel].push({
    id: 'set:' + rootId,
    code: '集合',
    title: '集合',
    type: 'set',
    children: relatedNodes
  })
  const addEdges = getEdgesByNodes(relatedNodes, edges.value, 'set:' + rootId)
  console.log('🚀 ~ findRelatedNode ~ addEdges:===》\n', addEdges)
  setNodes()
  nextTick(() => {
    edges.value?.push(...addEdges)
  })
}

// 更新节点位置
function updateNodePosition(nodes: Node[]) {
  console.log('🚀 ~ updateNodePosition ~ nodes:===》\n', nodes)
  const levelMap: number[][] = []
  for (let index = 0; index < nodes.length; index++) {
    const node = nodes[index]
    const { levelI } = node.data
    if (levelMap[levelI] == null) levelMap[levelI] = []
    levelMap[levelI].push(index)
  }
  console.log('🚀 ~ updateNodePosition ~ levelMap:===》\n', levelMap)
  let levelStartY = {} // 每一层起始 y 坐标
  let levelMaxWidth: { [level: string]: number } = {} // 每一层的最宽节点
  for (let index = 0; index < levelMap.length; index++) {
    const oneLevel = levelMap[index] // 某一层
    const count = oneLevel.length // 当前层的节点数量
    let oneLevelHeight = 0 // 当前层节点总高度
    let oneLevelMaxWidth = 0 // 当前层的最宽节点的宽度
    for (let index = 0; index < oneLevel.length; index++) {
      const nodei = oneLevel[index]
      oneLevelHeight += nodes[nodei].data.size?.height || NodeSize.height
      const nodeWidth = nodes[nodei].data.size?.width || NodeSize.width
      if (oneLevelMaxWidth < nodeWidth) {
        oneLevelMaxWidth = nodeWidth
      }
    }
    levelMaxWidth[index] = oneLevelMaxWidth
  }

  // TODO 获取某一层的起始 y 位置 , 当节点更窄时，需要进一步计算位置
}

// 更新相关节点的关系
function updateRelatedNode(rootId: string) {
  const preLevel = Number(rootId.split('-')[0]) - 1
  if (preLevel < 0) return
  const setId = 'set:' + rootId
  // 添加一个集合节点
  nodes.value.push({
    id: setId,
    position: { x: 0, y: 0 },
    data: {
      levelI: preLevel,
      size: {
        width: NodeSize.width * columnItems[rootId],
        height: NodeSize.height * columnItems[rootId]
      }
    },
    type: 'set'
  })

  // 设置关联节点的父级节点 = 新的集合节点
  const relatedEdges = edges.value.filter((edge) => edge.target == rootId)
  const relatedNodes = relatedEdges.map((edge) => {
    return nodes.value.find((node) => node.id == edge.source)
  })
  for (let index = 0; index < relatedEdges.length; index++) {
    const edge = relatedEdges[index]
    nodes.value?.forEach((node) => {
      if (node.id == edge.source) {
        node.parentNode = setId
      }
    })
  }

  updateNodePosition(nodes.value)

  const addEdges = getEdgesByNodes(relatedNodes, edges.value, setId)
  nextTick(() => {
    edges.value?.push(...addEdges)
  })
}

// 获取节点关联的所有边
function getEdgesByNodes(nodes: any[], edges: Edge[], setId: string) {
  const replaceEdges: Edge[] = [] // 新节点，需要补充的边
  nodes.forEach((node) => {
    for (let index = 0; index < edges.length; index++) {
      const edge = edges[index]
      let newEdge: Edge | undefined = undefined
      if (edge.source == node.id) {
        newEdge = {
          id: `${setId}->${edge.target}`,
          source: setId,
          target: edge.target,
          animated: true
        }
        if (nodeWithRelate[node.id]?.next == null) {
          nodeWithRelate[node.id]['next'] = []
        }
        if (!nodeWithRelate[node.id]['next'].includes(edge.target))
          nodeWithRelate[node.id]['next'].push(edge.target)
      } else if (edge.target == node.id) {
        newEdge = {
          id: `${edge.source}->${setId}`,
          source: edge.source,
          target: setId,
          animated: true
        }
        if (nodeWithRelate[node.id]?.pre == null)
          nodeWithRelate[node.id] = {
            pre: []
          }
        if (!nodeWithRelate[node.id]['pre'].includes(edge.source))
          nodeWithRelate[node.id]['pre'].push(edge.source)
      }
      if (newEdge) {
        replaceEdges.find((edge) => edge.id == newEdge!.id) == null && replaceEdges.push(newEdge)
      }
    }
  })
  return replaceEdges
}

function hover(node: Node) {
  nodes.value?.push(node)
}
onMounted(() => {
  setNodes()
  initEdges()
})
</script>

<template>
  <VueFlow :nodes="nodes" :edges="edges">
    <!-- bind your custom node type to a component by using slots, slot names are always `node-<type>` -->
    <template #node-end="props">
      <EndNode
        :id="props.id"
        :data="props.data"
        :col-number="columnItems[props.id]"
        @update:col-number="changeLayout"
      />
    </template>
    <template #node-set="props">
      <SetNode
        :id="props.id"
        :data="props.data"
        :col-number="columnItems[props.id.split(':')[1]]"
        @hover="hover"
      />
    </template>

    <!-- bind your custom edge type to a component by using slots, slot names are always `edge-<type>` -->
    <!-- <template #edge-special="specialEdgeProps">
      <SpecialEdge v-bind="specialEdgeProps" />
    </template> -->
  </VueFlow>
</template>

<style>
/* import the necessary styles for Vue Flow to work */
@import '@vue-flow/core/dist/style.css';

/* import the default theme, this is optional but generally recommended */
@import '@vue-flow/core/dist/theme-default.css';

.vue-flow__node-toolbar {
  display: flex;
  gap: 0.5rem;
  align-items: center;
  background-color: #2d3748;
  padding: 8px;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.5);
}

.vue-flow__node-end {
  width: 152px;
  height: 42px;
  border: 1px solid purple;
  border-radius: 3px;
  font-size: 12px;
  text-align: center;
  line-height: 42px;
}

.vue-flow__node-end.selected {
  box-shadow: 0 0 0 2px #2563eb;
}
</style>
