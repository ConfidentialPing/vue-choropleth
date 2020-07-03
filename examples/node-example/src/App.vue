<template>
  <div id="app">
    <l-map :center="[52, -98.5795]" :zoom="3" style="height: 500px;" :options="mapOptions">
      <l-choropleth-layer :data="pyDepartmentsData" titleKey="department_name" idKey="department_id" :value="value" :extraValues="extraValues" geojsonIdKey="dpto" :geojson="paraguayGeojson" :colorScale="colorScale">
        <template slot-scope="props">
          <l-info-control :item="props.currentItem" :unit="props.unit" title="Department" placeholder="Hover over a department"/>
          <l-reference-chart title="Girls school enrolment" :colorScale="colorScale" :min="props.min" :max="props.max" position="topright"/>
        </template>
      </l-choropleth-layer>
    </l-map>
  </div>
</template>

<script>
import { InfoControl, ReferenceChart, ChoroplethLayer } from 'vue-choropleth'

import { geojson } from './data/us-departments-geojson-4'
import paraguayGeojson from './data/usa-4.json'
import { pyDepartmentsData } from './data/us-departments-data-4'
import {LMap} from 'vue2-leaflet';

export default {
  name: "app",
  components: { 
    LMap,
    'l-info-control': InfoControl, 
    'l-reference-chart': ReferenceChart, 
    'l-choropleth-layer': ChoroplethLayer 
  },
  data() {
    return {
      pyDepartmentsData,
      paraguayGeojson,
      colorScale: ["FFFF00","00FF80", "0000FF"],
      value: {
        key: "amount_m",
        metric: "% boys"
      },
      extraValues: [{
        key: "amount_w",
        metric: "% girls"
      }],
      mapOptions: {
        attributionControl: false
      },
      currentStrokeColor: '3d3213'
    }
  },
}
</script>
<style>
@import "../node_modules/leaflet/dist/leaflet.css";
body {
  background-color: #e7d090;
  margin-left: 100px;
  margin-right: 100px;
}

#map {
  background-color: #eee;
}
</style>
