<template>
  <div id="app">
    <div style="height: 500px; width: 800px; border: 1px solid red; position: relative;margin: 0 auto;">
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :isConflictCheck="true"
        :snap="true"
        :snapTolerance="1"
        @refLineParams="getRefLineParams"
        :isRotateHandlerShow="true"
        @rotate="getRotate"
        class="test1">
      </vue-draggable-resizable>
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :x="210"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :isConflictCheck="true"
        :snap="true"
        :snapTolerance="1"
        :isRotateHandlerShow="true"
        @rotating="getRotate"
        :angle='20'
        @refLineParams="getRefLineParams"
        class="test2">
        <div slot="rotateHandle">
        Aa
        </div>
      </vue-draggable-resizable>
      <vue-draggable-resizable
        :w="200"
        :h="200"
        :parent="true"
        :x="420"
        :debug="false"
        :min-width="200"
        :min-height="200"
        :isConflictCheck="true"
        :snap="true"
        :isRotateHandlerShow="true"
        @rotating="getRotate"
        @rotated="getRotate2"
        :angle='angle'
        :snapTolerance="1"
        @refLineParams="getRefLineParams"
        class="test3">
      </vue-draggable-resizable>
      <!--辅助线-->
      <span class="ref-line v-line"
            v-for="item in vLine"
            :key="item.id"
            v-show="item.display"
            :style="{ left: item.position, top: item.origin, height: item.lineLength}"
      />
      <span class="ref-line h-line"
            v-for="item in hLine"
            :key="item.id"
            v-show="item.display"
            :style="{ top: item.position, left: item.origin, width: item.lineLength}"
      />
      <!--辅助线END-->
    </div>
    <input v-model="angle">
  </div>
</template>

<script>
import VueDraggableResizable from './components/vue-draggable-resizable'
import './components/vue-draggable-resizable.css'
export default {
  name: 'app',
  components: {
    VueDraggableResizable
  },
  data () {
    return {
      angle: 0,
      vLine: [],
      hLine: []
    }
  },
  methods: {
    getRotate (angle) {
      this.angle = angle
    },
    getRotate2 (angle) {
      this.angle = angle
    },
    // 辅助线回调事件
    getRefLineParams (params) {
      const { vLine, hLine } = params
      let id = 0
      this.vLine = vLine.map(item => {
        item['id'] = ++id
        return item
      })
      this.hLine = hLine.map(item => {
        item['id'] = ++id
        return item
      })
    }
  }
}
</script>

<style>
  .test1 {
    background-color: rgb(239, 154, 154);
  }
  .test2{
    background-color: rgb(129, 212, 250);
  }
  .test3{
    background-color: rgb(174, 213, 129);
  }
</style>
