<template>
  <Suspense>
    <template #default>
      <CalorieTracker />
    </template>
    <template #fallback>
      <div>Loading...</div>
    </template>
  </Suspense>
</template>

<script>
import { Client, provideClient, cacheExchange, fetchExchange } from '@urql/vue';
import CalorieTracker from './components/CalorieTracker.vue'

export default {
  name: 'App',
  components: { CalorieTracker },
  beforeMount() {
    provideClient(new Client({
      url: 'https://balanced-weevil-66.hasura.app/v1/graphql',
      exchanges: [cacheExchange, fetchExchange],
      fetchOptions: () => {
        return {
          headers: {
            "x-hasura-admin-secret": "nkJ7VZ4zP4d9qEIfjVp3U6xfWxDgLdKxYqgxfeALTrXsDQnvq810OSqffD2TGRmz",
          },
        };
      },
    }));
  },
}
</script>
