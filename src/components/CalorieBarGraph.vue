<template>
  <h1>Calories per Day</h1>
  <div class="canvas-container" style="aspect-ratio: 2 / 1">
    <Bar id="calorie-bar-graph" :data="chartData" :options="chartOptions" />
  </div>
</template>

<script>
import { Bar } from 'vue-chartjs';
import { Chart as ChartJS, Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, Colors } from 'chart.js';

ChartJS.register(Title, Tooltip, Legend, BarElement, CategoryScale, LinearScale, Colors);
const white = 'rgba(255, 255, 255, 0.87)';

export default {
  name: 'CalorieBarGraph',
  components: { Bar },
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
        scales: {
          x: {
            stacked: true,
            ticks: { color: white },
          },
          y: {
            stacked: true,
            ticks: { color: white },
          },
        },
      },
    };
  },
  computed: {
    chartData() {
      const dataMap = new Map();
      for (let meal of this.meals) {
        let entry = dataMap.get(meal.date) || {Breakfast: 0, Lunch: 0, Dinner: 0};
        entry[meal.meal] = meal.calories;
        dataMap.set(meal.date, entry);
      }
      const dataset = Array.from(dataMap.values());
      return {
        labels: Array.from(dataMap.keys()).map(date => date.substring(6)),
        datasets: [
          {
            label: 'Breakfast',
            data: dataset.map(_ => _.Breakfast),
          },
          {
            label: 'Lunch',
            data: dataset.map(_ => _.Lunch),
          },
          {
            label: 'Dinner',
            data: dataset.map(_ => _.Dinner),
          },
        ],
      };
    },
  },
}
</script>
