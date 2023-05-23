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
    meals: { required: true, type: Array },
  },
}
</script>

<style scoped lang="scss">
$border-color: rgba(255, 255, 255, 0.87);

table {
  border-collapse: collapse;
  border: 1px solid $border-color;
  display: flex;
  flex-direction: column;
  flex: 1;
  max-height: 1046px;
  overflow: hidden;
}
tbody {
  overflow: auto;
}
th, td {
  border: 1px solid $border-color;
  padding: 15px;
}
th {
  border-bottom: 3px solid $border-color;
}
tr > :nth-child(1) {
  width: 82px;
}
tr > :nth-child(2) {
  width: 65px;
}
tr > :nth-child(3) {
  text-align: right;
  width: 52px;
}
@media only screen and (min-height: 1317px) {
  tr > :nth-child(3) {
    width: 60px;
  }
}
</style>
