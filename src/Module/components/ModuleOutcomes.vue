<template>
  <v-container class="module-outcomes">
    <div class="module-outcomes__container">
      <h2 class="firstSetting">
      Minimum amount of links required to read before unlocking next step</h2>
      <br/>
          <v-overflow-btn
            class="firstDropdown"
            :items="linkNumbers"
            label="Number of Links"
          ></v-overflow-btn>
      <br/>
      <br/>
      <br/>
      <br/>
      <h2 class="secondSetting">Minimum number of templates required to
         create before unlocking next step</h2>
      <br/>
          <v-overflow-btn
            class="secondDropdown"
            :items="templateNumbers"
            label="Number of Templates"
          ></v-overflow-btn>
      <br/>
      <br/>
      <br/>
      <br/>
      <v-btn class="firstButton" depressed large outlined color="grey lighten-3"
      style="
            border: 1px solid #828282;
            border-radius: 10px;
            padding-top:0px;
            height: 40px;
            width: 200px;
            font-weight: 800;
            font-size: 16px;
            color:#828282 !important;">Discard</v-btn>
      <v-btn class="secondButton" depressed large outlined color="grey darken-4"
      style="
            border: 1px solid #828282;
            border-radius: 10px;
            padding-top:0px;
            height: 40px;
            width: 200px;
            font-weight: 800;
            font-size: 16px;
            color:#000000 !important;">Save</v-btn>
    </div>
  </v-container>
</template>

<script lang="ts">
import Vue from 'vue';
// import gql from 'graphql-tag';

export default Vue.extend({
  name: 'ModuleOutcomes',
  apollo: {
  },
  data: () => ({
    linkNumbers: ['1 link', '2 links', '3 links'],
    templateNumbers: ['1 template', '2 templates', '3 templates',
      '4 templates', '5 templates', '6 templates',
      '7 templates', '8 templates', '9 templates', '10 templates'],
  }),
});
</script>

<style>
.module-outcomes__container {
  width: 100%;
  max-width: 580px;
}
h2.firstSetting {
  position: center;
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 15px;
  width: 100%;
  padding-left:30px;
}
h2.secondSetting {
  position: center;
  font-family: 'Raleway', sans-serif;
  font-weight: 800;
  font-size: 15px;
  width: 100%;
}
.v-btn.firstButton {
 left: 70px;
}
.v-btn.secondButton {
  left: 110px;
}
input[type="hidden" i] {
    display: block !important;
}
div.v-input.firstDropdown {
  left: 170px;
  width: 40%;
}
div.v-input.secondDropdown {
  left: 170px;
  width: 40%;
}
.v-application .primary--text {
  color: #01579B var(--v-light-blue darken-4
) !important;
  caret-color: #01579B var(--v-light-blue darken-4
) !important;
}
.v-select__selection--comma {
  overflow: visible !important;
}
div.v-list-item_title {
  color: #01579B !important;
}
</style>
