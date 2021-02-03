<template>
  <v-stage
    ref="stage"
    :config="configKonva"
    @dragstart="handleDragstart"
    @dragend="handleDragend"
  >
    <v-layer ref="layer">
      <v-module
        v-for="item in list"
        :key="item.id"
        :config="{
          x: item.x,
          y: item.y,
          id: item.id,
          numPoints: 5,
          innerRadius: 30,
          outerRadius: 50,
          fill: '#89b717',
          opacity: 0.8,
          draggable: true,
          scaleX: dragItemId === item.id ? item.scale * 1.2 : item.scale,
          scaleY: dragItemId === item.id ? item.scale * 1.2 : item.scale,
          shadowColor: 'black',
          shadowBlur: 10,
          shadowOffsetX: dragItemId === item.id ? 15 : 5,
          shadowOffsetY: dragItemId === item.id ? 15 : 5,
          shadowOpacity: 0.6,
        }"
      ></v-module>
    </v-layer>
  </v-stage>
</template>

<script>
const width = window.innerWidth;
const height = window.innerHeight;
export default {
  name: "App",
  components: {},
  data() {
    return {
      list: [],
      dragItemId: null,
      configKonva: {
        width: width,
        height: height,
      },
    };
  },
  methods: {
    handleDragstart(e) {
      // save drag element:
      this.dragItemId = e.target.id();
      // move current element to the top:
      const item = this.list.find((i) => i.id === this.dragItemId);
      const index = this.list.indexOf(item);
      this.list.splice(index, 1);
      this.list.push(item);
    },
    handleDragend(e) {
      this.dragItemId = null;
    },
  },
  mounted() {},
};
</script>

<style>
</style>
