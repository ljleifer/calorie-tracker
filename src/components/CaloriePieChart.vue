<template>
  <h1>Average Calories per Meal</h1>
  <div class="canvas-container" style="aspect-ratio: 1 / 1">
    <Pie id="calorie-pie-chart" :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { Pie } from 'vue-chartjs';
import { Chart as ChartJS, ArcElement, Tooltip, Legend } from 'chart.js';

ChartJS.register(ArcElement, Tooltip, Legend);
const white = 'rgba(255, 255, 255, 0.87)';

export default {
  name: 'CaloriePieChart',
  components: { Pie },
  props: {
    meals: { required: true, type: Array },
  },
  data() {
    return {
      chartOptions: {
        plugins: {
          legend: {
            display: true,
            labels: { color: white },
          },
        },
        responsive: true,
      },
    };
  },
  computed: {
    chartData() {
      return {
        labels: ['Breakfast', 'Lunch', 'Dinner'],
        datasets: [
          {
            data: [
              this.averageCaloriesForMeal('Breakfast'),
              this.averageCaloriesForMeal('Lunch'),
              this.averageCaloriesForMeal('Dinner'),
            ],
          },
        ],
      };
    },
  },
  methods: {
    /**
     * Returns average number of calories for meal type
     * @param {string} mealName
     * @returns {number}
     */
    averageCaloriesForMeal(mealName) {
      const caloriesInMeal = this.meals.filter(_ => _.meal === mealName).map(_ => _.calories);
      return caloriesInMeal.reduce((a, b) => a + b) / caloriesInMeal.length;
    }
  },
}
</script>
