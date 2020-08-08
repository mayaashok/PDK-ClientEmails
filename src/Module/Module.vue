<template>
<!--  TODO: make the inputs into actual components -->
  <v-container class="module">
    <div class="module__container">
      <div class="module__title">
        <div class="module__image rounded-circle">
          <v-icon large color="#7EC291" style="font-size:100px">mdi-email</v-icon>
        </div>
        <div class="module__header text-md-h5 text-sm-subtitle-1 d-flex align-end">
          <input type="text" class="module__header-text" :value="moduleName">
        </div>
      </div>
      <div class="module__body">
        <div class="module__pagination">
          <div
          :class="{'active': currentPage==page}"
          v-for="page in pages" :key="page">
            <div class="module__pagination-button--active"/>
            <v-btn
            :ripple="false"
            class="module__pagination-button elevation-0"
            color="transparent" height="40" small
            @click="currentPage=page">
              {{ page }}
            </v-btn>
          </div>
        </div>
        <div class="module__page">
          <keep-alive>
            <component :is="getComponent"/>
          </keep-alive>
        </div>
      </div>
    </div>
  </v-container>
</template>
<script lang="ts">
import Vue from 'vue';
import '@/styles/module.scss';
import * as Module from './components';

export default Vue.extend({
  name: 'Microapp',
  components: {
    'module-instruct': Module.Instruct,
    'module-metrics': Module.Metrics,
    'module-edit': Module.Edit,
    'module-outcomes': Module.Outcomes,
    'module-preview': Module.Default,
  },
  data: () => ({
    moduleName: 'Client Emails',
    pages: ['Metrics', 'Instruct', 'Outcomes', 'edit', 'Preview'],
    currentPage: 'Instruct',
  }),
  computed: {
    getComponent() {
      return `module-${this.currentPage.toLowerCase()}`;
    },
  },
});
</script>
