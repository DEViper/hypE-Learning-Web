<template>
  <v-container
    class="text-center"
    fill-height
    style="height: calc(100vh - 58px);"
  >
    <v-row align="center">
      <v-col>
        <h1 class="display-2 error--text">Ups!</h1>

        <p>Do tej strony nie masz dostępu</p>

        <router-link :to="{ name: 'Home' }">
          <v-btn rounded color="primary">
            Wróć do strony głównej
          </v-btn>
        </router-link>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: "NoPermission",
};
</script>
