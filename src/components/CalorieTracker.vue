<template>
  <template v-if="queryData?.meals?.length">
    <div class="navigation">
      <div :id="views.BAR_GRAPH" class="button" @click="setCurrentView(views.BAR_GRAPH)" :style="`background: rgb(54, 162, 235)`">Bar Graph</div>
      <div :id="views.PIE_CHART" class="button" @click="setCurrentView(views.PIE_CHART)">Pie Chart</div>
      <div :id="views.TABLE_DATA" class="button" @click="setCurrentView(views.TABLE_DATA)">Data Table</div>
    </div>
    <CalorieBarGraph v-if="isCurrentView(views.BAR_GRAPH)" :meals="queryData.meals" />
    <CaloriePieChart v-if="isCurrentView(views.PIE_CHART)" :meals="queryData.meals" />
    <CalorieTable v-if="isCurrentView(views.TABLE_DATA)" :meals="queryData.meals" />
  </template>
  <h1 v-else-if="queryData === null">Fetching Meals...</h1>
  <h1 v-else>Error Fetching Meals</h1>
</template>

<script>
import { gql, useQuery } from '@urql/vue';
import CalorieBarGraph from './CalorieBarGraph.vue';
import CaloriePieChart from './CaloriePieChart.vue';
import CalorieTable from './CalorieTable.vue';

const VIEWS = Object.freeze({
  BAR_GRAPH: 0,
  PIE_CHART: 1,
  TABLE_DATA: 2,
});

export default {
  name: 'CalorieTracker',
  components: { CalorieBarGraph, CaloriePieChart, CalorieTable },
  data() {
    return {
      currentView: VIEWS.BAR_GRAPH,
      queryData: null,
      views: VIEWS,
    };
  },
  methods: {
    /**
     * Return true if param matches current view
     * @param {number} view 
     * @returns {boolean}
     */
    isCurrentView(view) {
      return view === this.currentView;
    },
    /**
     * Change view to new component
     * Update current navigation pill highlight
     * @param {number} view 
     */
    setCurrentView(view) {
      let viewElem = document.getElementById(this.currentView);
      viewElem.style.background = 'none';
      this.currentView = view;
      viewElem = document.getElementById(this.currentView);
      viewElem.style.background = 'rgb(54, 162, 235)';
    }
  },
  async beforeMount() {
    const limit = 100;
    this.queryData = (await useQuery({
      query: gql`
        query ($limit: Int!) {
          meals(limit: $limit) {
            date
            meal
            calories
          }
        }
      `,
      variables: { limit },
    })).data;
  },
}
</script>

<style scoped>
.button {
  border: 1px solid rgba(255, 255, 255, 0.87);
  border-radius: 10px;
  cursor: pointer;
  margin: 0px 20px;
  padding: 10px;
}
.navigation {
  display: flex;
  justify-content: center;
}
</style>
