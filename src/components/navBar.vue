<template>
  <v-app-bar app color="brown lighten-1">
    <v-avatar size="85" tile>
      <v-img :src="logo" contain />
    </v-avatar>

    <div class="title ml-2">Biblioteca</div>

    <v-spacer></v-spacer>
    <v-row>
      <v-col cols="3" md="3" offset="3">
        <router-link to="/" class="title options">Home</router-link>
      </v-col>

      <v-col cols="3" md="3">
        <router-link to="/books" class="title options">Libros</router-link>
      </v-col>

      <v-col cols="3" md="3">
        <router-link to="/register" class="title options">Registro</router-link>
      </v-col>
    </v-row>
  </v-app-bar>
</template>

<script>
export default {
  name: "navBar",
  props: {
    logo: String,
  },
  methods: {
    goHome() {
      this.$router.push({ name: "home" });
    },
    goBooks() {
      this.$router.push({ name: "books" });
    },
  },
};
</script>

<style lang="sass" scoped>
.options
    text-decoration: none
    color: black
</style>
