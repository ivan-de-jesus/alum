<template>
<v-col cols="auto">
    <v-dialog transition="dialog-top-transition" max-width="600">
        <template v-slot:activator="{ on, attrs }">
            <v-btn align="center" color="primary" v-bind="attrs" v-on="on">Ayuda</v-btn>
        </template>
        <template  v-slot:default="dialog">
            <v-card>
                <v-toolbar color="primary" dark>Ayuda </v-toolbar>
                <v-card-text >
                    <div class="text-h2 pa-12">{{ayuda.help}}</div>
                </v-card-text>
                <v-card-actions class="justify-end">
                    <v-btn text @click="dialog.value = false">Cerrar</v-btn>
                </v-card-actions>
            </v-card>
        </template>
    </v-dialog>
</v-col>
</template>

<script>
export default {
    name: "Dialog",
    components: {

    },

    data: () => ({
        ayuda: ""
    }),
    created() {

        this.getExercises();

    },
    methods: {
        async getExercises() {
            const res = await this.axios.get("http://localhost:3000/exercises");
            this.ayuda = res.data[0];
            console.log("Ayuda", this.ayuda.help);

        },

    },
};
</script>

<!--<style>
#exagono {
    background: url("../assets/celdas.png");
    width: 50%;
    height: 50%;
    position: fixed;
    background-size: 100% 100%;
}
</style>-->
