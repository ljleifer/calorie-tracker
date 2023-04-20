<template>
  <div>
    <table v-if="meals">
      <thead>
        <tr>
          <th>Meal</th>
          <th>Calories</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="meal in meals.meals" :key="meal.id">
          <td>{{ meal.meal }}</td>
          <td>{{ meal.calories }}</td>
        </tr>
      </tbody>
    </table>
    <h1 v-else>Error Fetching Meals</h1>
  </div>
</template>

<script>
import { gql, useQuery } from '@urql/vue';

export default {
  name: 'CalorieTracker',
  async setup() {
    const date = '2023-04-15';
    const meals = await useQuery({
      query: gql`
        query ($date: date!) {
          meals(where: {date: {_eq: $date}}) {
            id
            date
            meal
            calories
          }
        }
      `,
      variables: { date },
    });
    return {
      meals: meals.data,
    };
  },
}
</script>
