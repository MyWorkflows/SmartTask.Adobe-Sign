<script lang="ts">
import { defineComponent, ref } from "vue";
import { VueFlow,Elements,MarkerType } from '@braks/vue-flow';
import "@braks/vue-flow/dist/style.css";
import "@braks/vue-flow/dist/theme-default.css";

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
