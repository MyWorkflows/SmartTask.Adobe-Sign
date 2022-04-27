<script lang="ts">
import { defineComponent } from "vue";
import { VueFlow, Position } from '@braks/vue-flow';

export default defineComponent({

  components:{
    VueFlow
  },
  name: "SmartTaskComponent", // vue component name
  props: ['componentState', 'componentStatus'],
  data() {
    return { model: {}, 
    elements:[
  {
    id: '1',
    data: {
      label: 'node 1',
    },
    position: { x: 100, y: 100 },
    targetPosition: Position.Right
  },
  {
    id: '2',
    data: {
      label: 'node 2',
    },
    position: { x: 100, y: 200 },
    sourcePosition: Position.Left
  },
  {
    id: 'e1-2',
    label: 'default edge',
    target: '2',
    source: '1',
  },
]};
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
  setup() {},
});
</script>

<template>
  <VueFlow :elements="elements"></VueFlow>
</template>
