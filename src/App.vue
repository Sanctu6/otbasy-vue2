<template>
  <v-app>
    <v-main>
      <TransposeTable/>
    </v-main>
  </v-app>
</template>

<script>
import TransposeTable from './components/TransposeTable.vue';

export default {
  name: 'App',

  components: {
    TransposeTable
},

  data: () => ({
    //
  }),
};
</script>
