# 1.0.0
Basic structure in place, downloaded dependencies, able to hit Hasura Postgres DB using urql.
Basic query, render basic table (Meal/Calories) on page to prove full end-to-end working.

# 1.1.0
Query now fetches all data from DB at the beginning to avoid multiple calls.
Changed Vue code style from Composition API to Options API for structure and uniformity across components.
Updated basic table to now display full dataset with all columns (date/meal/calories)
Added bar graph that displays calorie intake per meal per day.
Added pie chart that displays average calorie intake per meal type.
Added navigation pills to move between these components.
