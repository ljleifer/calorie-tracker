<template>
  <h1>Meal Data</h1>
  <table>
    <tbody>
      <tr>
        <template v-for="key in Object.keys(meals[0])">
          <th v-if="key.substring(0,2) !== '__'">{{ key.substring(0,1).toUpperCase() + key.substring(1) }}</th>
        </template>
      </tr>
      <tr v-for="meal in meals" :key="meal.id">
        <template v-for="key in Object.keys(meal)">
          <td v-if="key.substring(0,2) !== '__'">{{ meal[key] }}</td>
        </template>
      </tr>
    </tbody>
  </table>
</template>

<script>
export default {
  name: 'GenericTable',
  props: {
    meals: { required: true, type: Array },
  },
}
</script>

<style scoped lang="scss">
@import "../style.scss";

$border-color: rgba(255, 255, 255, 0.87);

table {
  border-collapse: collapse;
  border: 1px solid $border-color;
  display: flex;
  flex-direction: column;
  flex: 1;
  max-height: 1046px;
  overflow: auto;
}
th, td {
  border: 1px solid $border-color;
  padding: 15px;
}
tbody > :nth-child(1) {
  background-color: $background-color;
  position: sticky;
  top: -1px;
}
</style>
