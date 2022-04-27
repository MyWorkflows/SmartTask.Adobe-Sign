<script lang="ts">
import { defineComponent, ref } from "vue";
import { VueFlow,Elements,MarkerType } from '@braks/vue-flow';

export default defineComponent({
  components:{
    VueFlow
  },
  name: "SmartTaskComponent", // vue component name
  props: ['componentState', 'componentStatus'],
  data() {
    return { model: {}, };
  },
  computed: {},
  methods: {
    async submitForm() {
      this.$emit("execute-smart-task", this.model);
    },
  },
  created() {
    if (this.componentState) {
      this.model = this.componentState;
    }
  },
  setup() {


const elements = ref<Elements>([
  { id: '1', type: 'input', label: 'Node 1', position: { x: 250, y: 5 } },
  { id: '2', type: 'output', label: 'Node 2', position: { x: 100, y: 100 } },
  { id: '3', label: 'Node 3', position: { x: 400, y: 100 } },
  { id: '4', label: 'Node 4', position: { x: 150, y: 200 } },
  { id: '5', type: 'output', label: 'Node 5', position: { x: 300, y: 300 } },
  { id: 'e1-2', source: '1', target: '2', animated: true },
  { id: 'e1-3', label: 'edge with arrowhead', source: '1', target: '3', markerEnd: MarkerType.Arrow },
  { 
    id: 'e4-5', 
    type: 'step', 
    label: 'step-edge', 
    source: '4', 
    target: '5', 
    style: { stroke: 'orange' }, 
    labelBgStyle: { fill: 'orange' } 
  },
  { id: 'e3-4', type: 'smoothstep', label: 'smoothstep-edge', source: '3', target: '4' },
]);
return{elements};
  },
});
</script>

<template>
<div style="height:100%">
  <VueFlow style="min-height:500px" :default-zoom="1.5" :min-zoom="0.2" :max-zoom="4" v-model="elements"></VueFlow>
  </div>
</template>


<style >
.vue-flow {
  position: relative;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.vue-flow__container {
  position: absolute;
  height: 100%;
  width: 100%;
  left: 0;
  top: 0;
}

.vue-flow__transformationpane {
  pointer-events: none;
  transform-origin: 0 0;
  z-index: 2;
}

.vue-flow__pane {
  z-index: 1;
}

.vue-flow__viewport {
  z-index: 4;
}

.vue-flow__selectionpane {
  z-index: 5;
}

.vue-flow__selection {
  position: absolute;
  top: 0;
  left: 0;
}

.vue-flow__edges {
  overflow: visible;
  pointer-events: none;
}

.vue-flow__edge {
  pointer-events: visibleStroke;
}

.vue-flow__edge.inactive {
    pointer-events: none;
  }

@-webkit-keyframes dashdraw {
  from {
    stroke-dashoffset: 10;
  }
}

@keyframes dashdraw {
  from {
    stroke-dashoffset: 10;
  }
}

.vue-flow__edge-path {
  fill: none;
}

.vue-flow__edge-textwrapper {
  pointer-events: all;
}

.vue-flow__edge-text {
  pointer-events: none;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
}

.vue-flow__connection {
  pointer-events: none;
}

.vue-flow__connection .animated {
    stroke-dasharray: 5;
    -webkit-animation: dashdraw 0.5s linear infinite;
            animation: dashdraw 0.5s linear infinite;
  }

.vue-flow__connection-path {
  fill: none;
}

.vue-flow__nodes {
  pointer-events: none;
  transform-origin: 0 0;
}

.vue-flow__node {
  position: absolute;
  -webkit-user-select: none;
     -moz-user-select: none;
      -ms-user-select: none;
          user-select: none;
  pointer-events: all;
  transform-origin: 0 0;
  box-sizing: border-box;
}

.vue-flow__nodesselection {
  z-index: 3;
  transform-origin: left top;
  pointer-events: none;
}

.vue-flow__nodesselection-rect {
     position: absolute;
     pointer-events: all;
     cursor: -webkit-grab;
     cursor: grab;
   }

.vue-flow__handle {
  pointer-events: none;
}

.vue-flow__handle.connectable {
    pointer-events: all;
  }

.vue-flow__handle-bottom {
  top: auto;
  left: 50%;
  bottom: -4px;
  transform: translate(-50%, 0);
}

.vue-flow__handle-top {
  left: 50%;
  top: -4px;
  transform: translate(-50%, 0);
}

.vue-flow__handle-left {
  top: 50%;
  left: -4px;
  transform: translate(0, -50%);
}

.vue-flow__handle-right {
  right: -4px;
  top: 50%;
  transform: translate(0, -50%);
}

.vue-flow__edgeupdater {
  cursor: move;
  pointer-events: all;
}

/* additional components */
.vue-flow__controls {
  position: absolute;
  z-index: 5;
  bottom: 10px;
  left: 10px;
}
.vue-flow__controls-button {
    width: 24px;
    height: 24px;
    border: none;
  }
.vue-flow__controls-button svg {
      width: 100%;
    }

.vue-flow__minimap {
  position: absolute;
  z-index: 5;
  bottom: 10px;
  right: 10px;
}

:root {
  --vf-node-bg: #fff;
  --vf-node-text: #222;
  --vf-connection-path:  #b1b1b7;
  --vf-handle: #555;
}

.vue-flow__selection {
  background: rgba(0, 89, 220, 0.08);
  border: 1px dotted rgba(0, 89, 220, 0.8);
}

.vue-flow__edge.selected .vue-flow__edge-path {
      stroke: #555;
    }

.vue-flow__edge.animated path {
    stroke-dasharray: 5;
    -webkit-animation: dashdraw 0.5s linear infinite;
            animation: dashdraw 0.5s linear infinite;
  }

.vue-flow__edge.updating .vue-flow__edge-path {
      stroke: #777;
    }

.vue-flow__edge-path {
  stroke: #b1b1b7;
  stroke-width: 1;
}

.vue-flow__edge-text {
  font-size: 10px;
}

.vue-flow__edge-textbg {
  fill: #fff;
}

.vue-flow__connection-path {
  stroke: var(--vf-connection-path);
  stroke-width: 1;
}

.vue-flow__node {
  cursor: -webkit-grab;
  cursor: grab;
}

.vue-flow__node-default,
.vue-flow__node-input,
.vue-flow__node-output {
  padding: 10px;
  border-radius: 3px;
  width: 150px;
  font-size: 12px;
  color: var(--vf-node-text);
  text-align: center;
  border-width: 1px;
  border-style: solid;

  background: var(--vf-node-bg);
  border-color: var(--vf-node-color);
}

.vue-flow__node-default.selected,
  .vue-flow__node-default.selected:hover,
  .vue-flow__node-input.selected,
  .vue-flow__node-input.selected:hover,
  .vue-flow__node-output.selected,
  .vue-flow__node-output.selected:hover {
     box-shadow: 0 0 0 0.5px var(--vf-box-shadow);
   }

.vue-flow__node-default .vue-flow__handle, .vue-flow__node-input .vue-flow__handle, .vue-flow__node-output .vue-flow__handle {
    background: var(--vf-handle);
  }

.vue-flow__node-default.selectable:hover, .vue-flow__node-input.selectable:hover, .vue-flow__node-output.selectable:hover {
    box-shadow: 0 1px 4px 1px rgba(0, 0, 0, 0.08);
  }

.vue-flow__node-input {
  --vf-node-color: #0041d0;
  --vf-handle: var(--vf-node-color);
  --vf-box-shadow: var(--vf-node-color);

  background: var(--vf-node-bg);
  border-color: var(--vf-node-color);
}

.vue-flow__node-default {
  --vf-node-color: #1a192b;
  --vf-handle: var(--vf-node-color);
  --vf-box-shadow: var(--vf-node-color);

  background: var(--vf-node-bg);
  border-color: var(--vf-node-color);
}

.vue-flow__node-output {
  --vf-node-color: #ff0072;
  --vf-handle: var(--vf-node-color);
  --vf-box-shadow: var(--vf-node-color);
}

.vue-flow__nodesselection-rect {
  background: rgba(0, 89, 220, 0.08);
  border: 1px dotted rgba(0, 89, 220, 0.8);
}

.vue-flow__handle {
  position: absolute;
  width: 6px;
  height: 6px;
  background: var(--vf-handle);
  border: 1px solid #fff;
  border-radius: 100%;
}

.vue-flow__handle.connectable {
    cursor: crosshair;
  }

.vue-flow__minimap {
  background-color: #fff;
}

.vue-flow__controls {
  box-shadow: 0 0 2px 1px rgba(0, 0, 0, 0.08);
}

.vue-flow__controls-button {
    background: #fefefe;
    border-bottom: 1px solid #eee;
    box-sizing: content-box;
    display: flex;
    justify-content: center;
    align-items: center;
    width: 16px;
    height: 16px;
    cursor: pointer;
    -webkit-user-select: none;
       -moz-user-select: none;
        -ms-user-select: none;
            user-select: none;
    padding: 5px;
  }

.vue-flow__controls-button svg {
      max-width: 12px;
      max-height: 12px;
    }

.vue-flow__controls-button:hover {
      background: #f4f4f4;
    }

</style>