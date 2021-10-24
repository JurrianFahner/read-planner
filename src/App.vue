<template>
  <v-app>
    <v-main>
      <read-planner />
    </v-main>
  </v-app>
</template>

<script>
import ReadPlanner from "@/components/ReadPlanner";

export default {
  name: 'App',

  components: {
    ReadPlanner,
  },

  data: () => ({
    //
  }),
};
</script>
