<template>
  <v-dialog v-model="dialog">
    <v-card>
      <v-card-title>Editar/Actualiza Libro</v-card-title>
      <v-card-text>
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field label="Autor" solo />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Titulo" solo  />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Edición" type="number" solo  />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Datos de publicación" solo  />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Tipo de Contenido" solo  />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Restricciones" solo  />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Materia" solo  />
          </v-col>
          <v-col cols="12" md="4">
            <v-text-field label="Proveedor" solo />
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
    name: 'update-book',
    props:{
        update: Boolean
    },
    data: () => ({
        dialog: false
    }),
    mounted(){
        this.dialog = this.update;
        console.log("prps",this.update);
    }
}
</script>
