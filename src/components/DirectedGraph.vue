<template>
  <div id="directed-graph">
    <svg :width="svgWidth" :height="svgHeight" @click="click" @mouseup="mouseup" @mousemove="mousemove" @mouseleave="leaveSVG">
      <circle v-for="node in nodes" :key="node.id" :cx="node.nodeCX" :cy="node.nodeCY" :r="node.nodeR" draggable="true" @mousedown="mousedown($event, node.id)" @mouseenter="mouseenter" @mouseleave="leaveNode"></circle>
    </svg>
  </div>
</template>

<script>
export default {
  name: 'directed-graph',
  data () {
    return {
      svgWidth: 300,
      svgHeight: 300,
      r: 10,
      nodes: [],
      isDragging: false,
      selectedNodeId: 0,
      isNode: false
    }
  },
  methods: {
    click (event) {
      if (this.isNode === false) {
        this.nodes.push({id: this.nodes.length, nodeCX: event.offsetX, nodeCY: event.offsetY, nodeR: this.r})
      }
    },
    mousedown (event, id) {
      this.selectedNodeId = id
      this.isDragging = true
    },
    mouseenter () {
      this.isNode = true
    },
    leaveNode () {
      this.isNode = false
    },
    mouseup (event) {
      this.isDragging = false
    },
    mousemove (event) {
      if (this.isDragging === true) {
        this.nodes[this.selectedNodeId].nodeCX = event.offsetX
        this.nodes[this.selectedNodeId].nodeCY = event.offsetY
        let x = this.nodes[this.selectedNodeId].nodeCX
        let y = this.nodes[this.selectedNodeId].nodeCY
        // svg外に移動で削除
        if (this.isRange(x, y) === false) {
          this.nodes.splice(this.selectedNodeId, 1)
          this.isNode = false
          this.isDragging = false
        }
      }
    },
    // svg外に移動で削除する場合はいらない？
    leaveSVG (event) {
      this.isDragging = false
    },
    isRange (x, y) {
      if (x >= this.svgWidth - 1 || x <= 1 || y >= this.svgHeight - 1 || y <= 1) {
        return false
      } else {
        return true
      }
    }
  }
}
</script>

<style>
svg {
  border: 1px solid rgba(0, 0, 0, 0.3);
}
circle {
  cursor: pointer;
}
</style>
