<template>
  <v-container>
    <v-card class="mt-10 brown lighten-3">
      <v-card-title class="text-center">Formulario de registro de un Libro</v-card-title>
      <v-card-text>
        <v-form @submit.prevent="insert">
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field label="Autor" solo v-model="book.autor" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Titulo" solo v-model="book.titulo" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Edición" type="number" solo v-model="book.edicion" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Datos de publicación" solo v-model="book.datos" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Tipo de Contenido" solo v-model="book.tipo" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Restricciones" solo v-model="book.restriccion" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Materia" solo v-model="book.materia" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Proveedor" solo v-model="book.proveedor" />
            </v-col>

            <v-btn class="info mt-3" large type="submit" :loading="loading"
              >Guardar</v-btn
            >
          </v-row>
        </v-form>
      </v-card-text>
    </v-card>

<!--Sucess Notification-->
    <v-dialog v-model="success" max-width="500" persistent>
      <v-card>
        <v-card-title class="text-h5 green accent-2">
          Libro registrado con exito!
          <v-spacer></v-spacer>
          <v-icon color="red" @click="success = false">mdi-close-thick</v-icon>
        </v-card-title>
      </v-card>
    </v-dialog>


<!--Error Notification-->
      <v-dialog v-model="error" max-width="650" persistent>
      <v-card>
        <v-card-title class="text-h5 red accent-2">
           <v-icon color="yellow">mdi-alert-box</v-icon>Debe de llenar todos los campos para el registro
          <v-spacer></v-spacer>
          <v-icon color="black" @click="error = false">mdi-close-thick</v-icon>
        </v-card-title>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  name: "register-books",
  data: () => ({
    book: {},
    success: false,
    loading: false,
    error: false,
  }),
  methods: {
    insert() {
      
      if (
        this.book.autor != null &&
        this.book.titulo != null &&
        this.book.edicion != null &&
        this.book.datos != null &&
        this.book.tipo != null &&
        this.book.restriccion != null &&
        this.book.materia != null &&
        this.book.proveedor != null
      ) {
        this.loading = true;
        this.$axios
          .get("/insert", {
            params: {
              data: this.book,
            },
          })
          .then(() => {})
          .catch(() => {})
          .finally(() => {
            this.loading = false;
            this.book = {};
            this.success = true;
          });
      } else {

        this.error = true;
      }
    },
  },
};
</script>
