<template>
  <v-container>
    <v-row>
      <v-col cols="12" md="6">
        <v-text-field
          v-model="search"
          append-icon="mdi-magnify"
          label="Buscar Libro..."
          single-line
          hide-details
        ></v-text-field>
      </v-col>
      <v-col cols="12" md="12" class="text-center">
        <v-data-table
          :headers="headers"
          :items="items"
          :items-per-page="5"
          :search="search"
        >
          <template v-slot:[`item.actions`]="{ item }">
            <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
            <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
          </template>
        </v-data-table>
      </v-col>
    </v-row>

    <v-dialog v-model="update" persistent>
      <v-card>
        <v-card-title
          ><v-icon color="red" @click="update = false">mdi-close-circle</v-icon
          >Editar/Actualiza Libro</v-card-title
        >
        <v-card-text>
          <v-row>
            <v-col cols="12" md="4">
              <v-text-field label="Autor" solo v-model="itemUpdate.autor" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Titulo" solo v-model="itemUpdate.titulo" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                label="Edición"
                type="number"
                solo
                v-model="itemUpdate.edicion"
              />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                label="Datos de publicación"
                solo
                v-model="itemUpdate.datos_publicacion"
              />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                label="Tipo de Contenido"
                solo
                v-model="itemUpdate.tipo_contenido"
              />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field
                label="Restricciones"
                solo
                v-model="itemUpdate.restricciones"
              />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Materia" solo v-model="itemUpdate.materia" />
            </v-col>
            <v-col cols="12" md="4">
              <v-text-field label="Proveedor" solo v-model="itemUpdate.proveedor" />
            </v-col>

            <v-col cols="12" md="4">
              <v-btn @click="updateItem" color="success" :loading="loadingEdit"
                >Actualizar Información</v-btn
              >
            </v-col>
          </v-row>
        </v-card-text>
      </v-card>
    </v-dialog>
  </v-container>
</template>

<script>
export default {
  name: "booksCrud",
  data: () => ({
    search: "",
    update: false,
    loadingEdit: false,
    items: [],
    itemUpdate: [],
    headers: [
      {
        text: "Folio Libro",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "id",
      },
      {
        text: "Autor",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "autor",
      },
      {
        text: "Titulo",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "titulo",
      },
      {
        text: "Edición",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "edicion",
      },
      {
        text: "Datos de publicación",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "datos_publicacion",
      },
      {
        text: "Tipo de Contenido",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "tipo_contenido",
      },
      {
        text: "Restricciones",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "restricciones",
      },
      {
        text: "Materia",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "materia",
      },
      {
        text: "Proveedor",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "proveedor",
      },
      {
        text: "Actions",
        align: "center",
        sortable: false,
        class: "light-blue lighten-4",
        value: "actions",
      },
    ],
  }),
  methods: {
    show() {
      this.$axios
        .get("/show", {})
        .then((response) => {
          this.items = response.data.books;
          console.log(this.items);
        })
        .catch(() => {})
        .finally(() => {});
    },
    editItem(item) {
      this.update = true;
      this.itemUpdate = Object.assign({}, item);
    },
    updateItem() {
      this.loadingEdit = true;
      this.$axios
        .post("/edit", {
          data: this.itemUpdate,
        })
        .then(() => {})
        .catch(() => {})
        .finally(() => {
          this.loadingEdit = false;
          this.show();
          this.update = false;
        });
    },
    deleteItem(item) {
      this.$axios
        .post("/delete", {
          data: item,
        })
        .then(() => {})
        .catch(() => {})
        .finally(() => {
          this.show();
        });
    },
  },
  mounted() {
    this.show();
  },
};
</script>
