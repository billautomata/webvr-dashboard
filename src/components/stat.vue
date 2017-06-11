<template>
  <a-entity id='stat'>
    <a-text font='roboto' align='center' scale='0.5 0.5 0.5' position='0 0 0' color='#000000' :value="label"></a-text>
    <a-text font='roboto' align='center' scale='2 2 0' position='0 0.25 0' color='#000000' :value="value"></a-text>
    <!-- <a-entity id='foo' geometry="primitive: box" material="color: red"></a-entity> -->
    <a-entity position='-0.25 -0.25 0' scale='1 0.2 0.2'>
      <a-box shadow geometry="primitive: box" :width='widths[0]' :position="[box_offsets[0], 0, 0].join(' ')" material="color: red; wireframe: false"></a-box>
      <a-box shadow geometry="primitive: box" :width='widths[1]' :position="[box_offsets[1] - widths[1] * 0.5, 0, 0].join(' ')" material="color: orange; wireframe: false"></a-box>
      <a-box shadow geometry="primitive: box" :width='widths[2]' :position="[box_offsets[2] - widths[2] * 0.5, 0, 0].join(' ')" material="color: yellow; wireframe: false"></a-box>
      <a-box shadow geometry="primitive: box" :width='widths[3]' :position="[box_offsets[3] - widths[3] * 0.5, 0, 0].join(' ')" material="color: blue; wireframe: false"></a-box>
    </a-entity>
  </a-entity>
</template>

<script>
export default {
  name: 'stat',
  props: [
    'label',
    'value',
    'stat_high',
    'stat_medium',
    'stat_low',
    'stat_pass'
  ],
  data () {
    return {
      stat_total: 0,
      box_offsets: [],
      widths: []
    }
  },
  mounted () {
    console.log(this.$el.querySelector('#foo'))
    window.k = this.$el.querySelector('#foo')
    this.stat_total = Number(this.stat_high) + Number(this.stat_medium) + Number(this.stat_low) + Number(this.stat_pass)
    var running_x = 0
    this.box_offsets.push(running_x)
    this.widths.push(this.stat_high / this.stat_total)
    running_x += (this.stat_high / this.stat_total)
    this.box_offsets.push(running_x)
    this.widths.push(this.stat_medium / this.stat_total)
    running_x += (this.stat_medium / this.stat_total)
    this.box_offsets.push(running_x)
    this.widths.push(this.stat_low / this.stat_total)
    running_x += (this.stat_low / this.stat_total)
    this.box_offsets.push(running_x)
    this.widths.push(this.stat_pass / this.stat_total)
    console.log(this.stat_total)
    console.log(this.box_offsets)
    console.log(this.widths)
    console.log(this.$el.object3D)
    window.k = (this.$el.object3D)
    this.$el.object3D.lookAt(new THREE.Vector3(1.0,100.0,1.0))
  }
}
</script>
