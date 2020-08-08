<template>
  <v-container class="module-metrics">
    <v-chip class="ma-1" color="grey lighten-1" text-color="white"
    style="width: 130px; height: 32px; left:115px;">
       <v-icon left small>mdi-close</v-icon>
    </v-chip>
    <v-chip class="ma-2" color="grey lighten-1" text-color="white"
    style="width: 130px; height: 32px; left:115px;">
      <v-icon left small>mdi-close</v-icon>
    </v-chip>
    <v-chip class="ma-3" style="width: 130px; height: 32px; left:115px;
    border:2px dashed #BDBDBD; color:white;">
    </v-chip>
    <div class="module-metrics__container" style="padding-left:35px;">
      <br/>
      <!-- <v-img src="MetricsGraph.png"></v-img> -->
      <v-card style="width:600px;">
        <v-container>
          <h2 style="font-weight:100; text-align:center; font-size:20px;">Metrics Graph Ex.</h2>
          <br/>
            <v-sparkline
              :labels="labels"
              :value="value"
              :gradient="gradient"
              :smooth="radius || false"
              :padding="padding"
              :line-width="lineWidth"
              :stroke-linecap="lineCap"
              :fill="fill"
              :type="type"
              :auto-line-width="autoLineWidth"
              auto-draw
              :show-labels="showLabels"
              :label-size="labelSize"
            ></v-sparkline>
          <br/>
            <v-divider></v-divider>
          <br/>
          <h3 style="font-weight:100; text-align:center; font-size:16px;">
          Number of Templates Created</h3>
        </v-container>
      </v-card>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
// import gql from 'graphql-tag';

// import Echarts from 'vue-echarts';

// import 'echarts/lib/chart/bar';

// Vue.component('chart', Echarts);

const gradients = [
  ['#BDBDBD'],
];

export default Vue.extend({
  name: 'ModuleMetrics',
  apollo: {
  },
  data: () => ({
    showLabels: true,
    lineWidth: 15,
    labelSize: 6,
    radius: 1,
    padding: 0,
    lineCap: 'square',
    gradient: gradients[0],
    value: [100, 75, 55, 64, 93, 48, 31, 87],
    labels: ['1', '2', '3', '4', '5', '6', '7', '8'],
    gradients,
    fill: true,
    type: 'bar',
    autoLineWidth: false,
  }),
});
</script>

<style>
.theme--light.v-chip:not(.v-chip--active) {
  background: white;
}
span.ma-3.v-chip.v-chip--no-color.theme--light.v-size--default {
  background: white;
}
</style>
