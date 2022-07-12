<template>
    <v-container>
        <v-row>
            <v-col cols="6" md="6" offset="3" class="mt-5">
                <v-img :src="logo" width="700"></v-img>
            </v-col>

            <v-col cols="12" md="12" class="text-center title">
                Plataforma de la biblioteca de la Universidad Metropolitana de Nuevo León
            </v-col>

            <v-col cols="12" md="12" class="text-center body-1">
                Esta página esta diseñada para la administración de la Universidad para el registro de sus libros
            </v-col>
        </v-row>
    </v-container>
</template>

<script>
export default {
    name: 'home-view',
    data: () => ({
        logo: require('../assets/logo.jpeg')
    })
}
</script>