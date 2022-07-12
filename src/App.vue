<template>
  <v-app>
    <NavBar :logo="img" />

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script>
import NavBar from './components/navBar.vue';

export default {
    name: "App",
    data: () => ({
    img: require('./assets/books.jpg')
    }),
    components: { NavBar },
};
</script>
