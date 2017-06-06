<template>
  <div id="app">
    <a-scene>
      <template v-for='(cube,index) in cubes'>
        <a-box :position="pos(index)" rotation="0 45 0" color="#4CC3D9"></a-box>
      </template>

      <a-sphere position="0 1.25 -5" radius="1.25" color="#EF2D5E"></a-sphere>
      <a-cylinder position="1 0.75 -3" radius="0.5" height="1.5" color="#FFC65D"></a-cylinder>
      <a-plane position="0 0 -4" rotation="-90 0 0" width="4" height="4" color="#7BC8A4"></a-plane>
      <a-text position='0 2 -3' color='#000000' :value="foo"></a-text>
      <a-sky color="#ECECEC"></a-sky>
    </a-scene>
  </div>
</template>

<script>
var aframe = require('aframe')

export default {
  name: 'app',
  components: {},
  data () {
    return {
      foo: '1',
      cubes: []
    }
  },
  mounted () {
    console.log(aframe)
    var self = this
    this.cubes.push(0)
    this.cubes.push(0)
    this.cubes.push(0)
    setInterval(function(){
      self.foo = Date.now()
    },1000)
  },
  methods: {
    pos: function(index){
      // console.log('pos', index)
      return [index * -1.5, 0.5, -3].join(' ')
    }
  }
}
</script>
