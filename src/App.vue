<template>
  <div id="app">
    <a-scene>
      <!-- <template v-for='(cube,index) in cubes'>
        <a-box :position="pos(index)" rotation="0 45 0" color="#4CC3D9"></a-box>
      </template> -->

      <a-entity position='0 1.5 -3'>
        <template v-for="(stat,index) in stats">
          <a-entity :rotation="[0, index * -5, 0].join(' ')" :position="[index*1.1, 0, 0].join(' ')">
            <stat v-bind:label='stat.label'
              v-bind:value='stat.value'
              v-bind:stat_high='2'
              v-bind:stat_medium='1'
              v-bind:stat_low='1'
              v-bind:stat_pass='1'></stat>
          </a-entity>
        </template>
        <!-- <stat label='us-west-2' value='128' stat_high='2' stat_medium='1' stat_low='1' stat_pass='1'></stat> -->
      </a-entity>
      <!-- <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-cylinder position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
      <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>
      <a-text position='0 2 -3' color='#000000' :value="foo"></a-text> -->
      <a-sky color="#ECECEC"></a-sky>

      <a-assets>
        <a-asset-item id="tree-obj" src="/obj/evident-shield.obj"></a-asset-item>
        <a-asset-item id="tree-mtl" src="/obj/evident-shield.mtl"></a-asset-item>
      </a-assets>
      <!-- <a-entity id='shield' position="0 2 -3" obj-model="obj: #tree-obj; mtl: #tree-mtl"></a-entity> -->
      <!-- <a-entity id='shield' position="0 2 -3" obj-model="obj: #tree-obj;" material="color: #3366ff; roughness: 1; metalness: 0"></a-entity> -->
      <!-- <a-entity id='shield' position="0 2 -3" obj-model="obj: #tree-obj;" material="shader: custom-material"></a-entity> -->

    </a-scene>
  </div>
</template>

<script>
var aframe = require('aframe')
import stat from './components/stat.vue'

export default {
  name: 'app',
  components: {
    stat
  },
  data () {
    return {
      foo: '1',
      cubes: [],
      stats: []
    }
  },
  beforeCreate () {
  },
  mounted () {
    console.log(aframe)
    var self = this

    // stats
    this.stats.push({
      label: 'us-west-2',
      value: '32',
      stat_high: '1',
      stat_medium: '2',
      stat_low: '3',
      stat_pass: '1'
    })
    this.stats.push({
      label: 'us-west-1',
      value: '100',
      stat_high: '1',
      stat_medium: '2',
      stat_low: '3',
      stat_pass: '1'
    })
    this.stats.push({
      label: 'us-east-2',
      value: '5',
      stat_high: '1',
      stat_medium: '2',
      stat_low: '3',
      stat_pass: '1'
    })


    this.cubes.push(0)
    this.cubes.push(0)
    this.cubes.push(0)
    setInterval(function(){
      self.foo = Date.now()
    },1000)
    // k.object3D.children[0].children[0].material.materials[0].color.g
  },
  methods: {
    pos: function(index){
      // console.log('pos', index)
      return [index * -1.5, 0.5, -3].join(' ')
    }
  }
}
</script>
