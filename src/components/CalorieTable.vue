<template>
  <h1>Meal Data</h1>
  <table>
    <thead>
      <tr>
        <th>Date</th>
        <th>Meal</th>
        <th>Calories</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="meal in meals" :key="meal.id">
        <td>{{ meal.date }}</td>
        <td>{{ meal.meal }}</td>
        <td>{{ meal.calories }}</td>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'CalorieTable',
  props: {
    meals: { required: true, type: Array, default: {} }
  },
}
</script>

<style scoped>
table {
  border-collapse: collapse;
  border: 1px solid rgba(255, 255, 255, 0.87);
  display: flex;
  flex-direction: column;
  flex: 1;
  overflow: hidden;
}
tbody {
  overflow: auto;
}
th, td {
  border: 1px solid rgba(255, 255, 255, 0.87);
  padding: 15px;
}
th {
  border-bottom: 3px solid rgba(255, 255, 255, 0.87);
}
tr > :nth-child(1) {
  width: 82px;
}
tr > :nth-child(2) {
  width: 65px;
}
tr > :nth-child(3) {
  width: 43px;
}
</style>
