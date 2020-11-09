<template>
  <v-app>
    <v-main>
      <RecrutationApp />
    </v-main>
  </v-app>
</template>

<script>
import RecrutationApp from "./components/RecrutationApp";

export default {
  name: "App",

  components: {
    RecrutationApp
  },

  data: () => ({
    //
  })
};
</script>
