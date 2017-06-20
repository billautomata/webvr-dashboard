<template>
  <div id="app">
    <a-scene effects="bloom, fxaa" bloom="radius: 0.66" fxaa>

      <a-assets>
        <a-asset-item id="tree-obj" src="obj/evident-shield.obj"></a-asset-item>
        <a-asset-item id="tree-mtl" src="obj/evident-shield.mtl"></a-asset-item>

        <a-asset-item id="esp-vr-satellite-mtl" src="obj/esp-vr-asset-satellite.mtl"></a-asset-item>
        <a-asset-item id="esp-vr-satellite-obj" src="obj/esp-vr-asset-satellite.obj"></a-asset-item>

        <a-asset-item id="vr-sat-json" src="obj/esp-vr-asset-satellite.json"></a-asset-item>
        <!-- <a-asset-item id="environment-obj" src="obj/environment.obj"></a-asset-item> -->
        <!-- <a-asset-item id="environment-mtl" src="obj/environment.mtl"></a-asset-item> -->
        <a-asset-item id="vr-environment-obj" src="obj/vr-environment.obj"></a-asset-item>
        <a-asset-item id="vr-environment-mtl" src="obj/vr-environment.mtl"></a-asset-item>

        <a-asset-item id="pyramid-obj" src="obj/pyramid.obj"></a-asset-item>
        <a-asset-item id="pyramid-mtl" src="obj/pyramid.mtl"></a-asset-item>

        <a-asset-item id="sphere-env-obj" src="obj/spherenvironment.obj"></a-asset-item>
        <a-asset-item id="sphere-env-mtl" src="obj/spherenvironment.mtl"></a-asset-item>
      </a-assets>

      <!-- <template v-for='(cube,index) in cubes'>
        <a-box :position="pos(index)" rotation="0 45 0" color="#4CC3D9"></a-box>
      </template> -->

      <a-entity position='1.7 1.5 -4'>
        <template v-for="(stat,index) in region_stats">
          <a-entity :rotation="[0, 0, 0].join(' ')" :position="grid_pos(index)"  scale='0 0 0'>
            <stat v-bind:label='stat.label'
              v-bind:value='stat.value'
              v-bind:stat_high='stat.stat_high'
              v-bind:stat_medium='stat.stat_medium'
              v-bind:stat_low='stat.stat_low'
              v-bind:stat_pass='stat.stat_pass'></stat>
              <a-animation attribute="scale"
                           :dur="1000 + (index*150)"
                           fill="forwards"
                           to="1 1 1"
                           repeat="0"></a-animation>
          </a-entity>
        </template>
      </a-entity>

      <a-entity position='-5 1.5 -4'>
        <template v-for="(stat,index) in services_stats">
          <a-entity :rotation="[0, 0, 0].join(' ')" :position="grid_pos(index)" scale='0 0 0'>
            <stat v-bind:label='stat.label'
              v-bind:value='stat.value'
              v-bind:stat_high='stat.stat_high'
              v-bind:stat_medium='stat.stat_medium'
              v-bind:stat_low='stat.stat_low'
              v-bind:stat_pass='stat.stat_pass'></stat>
              <a-animation attribute="scale"
                           :dur="1000 + (index*150)"
                           fill="forwards"
                           to="1 1 1"
                           repeat="0"></a-animation>
          </a-entity>
        </template>
      </a-entity>

      <a-entity geometry='primitive: sphere; segmentsWidth: 32; segmentsHeight: 32; radius: 9;' position='0 0 -15' scale='1 1 1' rotation='30 0 0'
      material="src: url(texture/earth.jpg); wireframe: false;">
        <a-animation attribute="rotation"
                     dur='100000'
                     fill="none"
                     to="30 360 0"
                     repeat="indefinite"
                     easing='linear'></a-animation>
      </a-entity>

      <a-sky color="#ECECEC"></a-sky>

      <a-entity>
        <template v-for='(sat,index) in sats' v-bind:sat='sat'>
          <a-entity :rotation="[0, 0, sat.rot].join(' ')">
            <a-entity rotatation='0 0 0' position="0 0 -15">
              <a-entity id='sat' shadow="cast: true; receive: true" :position="[0, 0, sat.distance].join(' ')">
                <a-entity scale='0.1 0.1 0.1' rotation='-90 0 0' json-model="src: url(./obj/esp-vr-asset-satellite.json);"></a-entity>
                <a-entity rotation='0 0 0'>
                  <a-entity scale='0.1 0.1 0.1' rotation='-90 0 0' json-model="src: url(./obj/sat-beam.json);"></a-entity>
                  <a-animation attribute="rotation"
                               dur='2000'
                               fill="none"
                               to="0 0 360"
                               repeat="indefinite"
                               easing='linear'></a-animation>
                </a-entity>
              </a-entity>
              <a-animation attribute="rotation"
                           :dur='sat.speed'
                           fill="none"
                           to="0 360 0"
                           repeat="indefinite"
                           easing='linear'></a-animation>
            </a-entity>
          </a-entity>
        </template>
      </a-entity>

      <a-entity id='shield' shadow="cast: true; receive: true" rotatation='0 0 0' position="0 2 -5" scale='0 0 0' obj-model="obj: #tree-obj; mtl: #tree-mtl">
        <a-animation attribute="scale"
                     dur='1000'
                     fill="forwards"
                     to="1 1 1"
                     repeat="0"
                     easing='ease-out-bounce'>
        </a-animation>
        <a-animation attribute="rotation"
                    dur='1000'
                    fill="forwards"
                    easing='ease-out-bounce'
                    to="360 0 0"
                    delay="4000"
                    repeat="indefinite">
        </a-animation>
        <a-animation attribute="rotation"
                     dur='700'
                     fill="forwards"
                     easing='ease-out-bounce'
                     from='360 0 0'
                     to="360 360 0"
                     delay="10000"
                     repeat="indefinite">
        </a-animation>
      </a-entity>
      <a-entity cubemap="folder: texture/cubemap/"></a-entity>
      <!-- <a-entity id='shield' position="0 2 -8" obj-model="obj: #tree-obj; mtl: #tree-mtl"></a-entity> -->

      <!-- <a-entity id='vr-environment' position="0 -2 0" obj-model="obj: #vr-environment-obj; mtl: #vr-environment-mtl;" shadow="cast: true; receive: true"></a-entity> -->
      <!-- <a-entity id='pyramid' position="0 -2.9 0" scale='2 2 2' obj-model="obj: #pyramid-obj;"  material="color: #3366ff; metalness: 0; roughness: 1" shadow="cast: true; receive: true"></a-entity> -->



      <!-- <a-entity id='sphere-env' position="0 8 0" obj-model="obj: #sphere-env-obj; mtl: #sphere-env-mtl;"></a-entity> -->
      <!-- <a-entity id='shield' position="0 2 -3" obj-model="obj: #tree-obj;" material="color: #3366ff; roughness: 1; metalness: 0"></a-entity> -->
      <!-- <a-entity id='shield' position="0 2 -3" obj-model="obj: #tree-obj;" material="shader: custom-material"></a-entity> -->
      <!-- <a-ocean color='purple' depth="100" width="100"></a-ocean> -->

      <!-- <a-light position='0.5 1 0.4' color="#333" distance="20" intensity="4" type="directional"></a-light> -->
      <!-- <a-entity light="castShadow: true; color: #FAFAFA; intensity: 1.0; shadowBias: 0.01
                       shadowCameraNear: 1; shadowCameraBias: 0.01;
                       type: directional; shadowMapWidth: 1024; shadowMapHeight: 1024"
                position="0.5 0.8 0"></a-entity> -->

      <!-- <a-light type="ambient" color="#ccc"></a-light> -->
      <a-light color="#ddf" position="0 20 5" distance="50" intensity="1" type="point" castShadow='true'></a-light>
    </a-scene>
  </div>
</template>

<script>
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
      region_stats: [],
      services_stats: [],
      summary_stats: [],
      sats: []
    }
  },
  beforeCreate () {
  },
  mounted () {

    this.sats.push({
      rot: 0,
      distance: 10,
      speed: 4300
    })
    this.sats.push({
      rot: 45,
      distance: 12,
      speed: 10000
    })
    this.sats.push({
      rot: 90,
      distance: 13,
      speed: 5800
    })
    this.sats.push({
      rot: 120,
      distance: 14,
      speed: 8000
    })

    console.log(AFRAME)
    var self = this

    var regions = ['us-west-2', 'us-east-2', 'ca-central-1', 'ap-south-1', 'global', 'eu-west-1', 'ap-northeast-1', 'ap-northeast-2']
    var services = ['IAM', 'RDS', 'EC2', 'Cloudformation', 'S3']
    var statuses = ['risks identified', 'high', 'medium', 'low', 'pass']

    regions.forEach(function(r){
      var stats = {
        stat_high: Number(Math.floor(Math.random()*64)),
        stat_medium: Number(Math.floor(Math.random()*64)),
        stat_low: Number(Math.floor(Math.random()*64)),
        stat_pass: Number(Math.floor(Math.random()*64)),
        label: r,
        value: String(Math.floor(Math.random()*256))
      }
      self.region_stats.push(stats)
    })

    services.forEach(function(r){
      var stats = {
        stat_high: Number(Math.floor(Math.random()*64)),
        stat_medium: Number(Math.floor(Math.random()*64)),
        stat_low: Number(Math.floor(Math.random()*64)),
        stat_pass: Number(Math.floor(Math.random()*64)),
        label: r,
        value: String(Math.floor(Math.random()*256))
      }
      self.services_stats.push(stats)
    })

    statuses.forEach(function(r){
      var stats = {
        label: r,
        value: String(Math.floor(Math.random()*256))
      }
      self.summary_stats.push(stats)
    })

    // k.object3D.children[0].children[0].material.materials[0].color.g
  },
  methods: {
    pos: function(index){
      // console.log('pos', index)
      return [index * -1.5, 0.5, -3].join(' ')
    },
    grid_pos: function(index){
      var grid_width = 4
      var space_multi = 1.1
      console.log('pos', index)
      var x = index % grid_width
      var y = Math.floor(index / grid_width)

      return [ x * space_multi, y * space_multi, 0 ].join(' ')
    }
  }
}
</script>
