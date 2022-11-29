<template>
  <v-stepper v-model="e1">
    <v-stepper-header>
      <v-stepper-step :complete="e1 > 1" step="1">
        Ejercicio #1
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step :complete="e1 > 2" step="2">
        Ejercicio #2
      </v-stepper-step>

      <v-divider></v-divider>

      <v-stepper-step step="3"> Ejercicio #3 </v-stepper-step>
    </v-stepper-header>

    <v-stepper-items>
      <v-stepper-content step="1">
        <v-card class="mb-12" color="#063A18" height="200px">
          <p v-if="this.asignado">
            {{ this.anuncio }}
          </p>
        </v-card>
        <v-row>
          <v-btn disabled="true" color="primary" @click="e1 = 2"> Continue </v-btn>

          <v-btn text> Cancel </v-btn>

          <Dialog></Dialog>
        </v-row>
      </v-stepper-content>

      <v-stepper-content step="2">
        <v-card class="mb-12" color="grey lighten-1" height="200px"></v-card>

        <v-btn color="primary" @click="e1 = 3"> Continue </v-btn>

        <v-btn text> Cancel </v-btn>
      </v-stepper-content>

      <v-stepper-content step="3">
        <v-card class="mb-12" color="grey lighten-1" height="200px"></v-card>

        <v-btn color="primary" @click="e1 = 1"> Continue </v-btn>

        <v-btn text> Cancel </v-btn>
      </v-stepper-content>
    </v-stepper-items>
  </v-stepper>
</template>

<script>
import Dialog from "./Dialog.vue";
export default {
  data() {
    return {
      e1: 1,
      anuncio: "",
      asignado: false
    };
  },

  components: { Dialog },
  created() {

    this.getExercises();
    this.getStudents();
  },
  methods: {
    async getExercises() {
      const res = await this.axios.get("http://localhost:3000/exercises");
      console.log("Entro al get ", res) 
      this.anuncio = res.data[0].instruction + " : " + res.data[0].exercise; 
      this.desserts = res.data;
    },
    async getStudents() {
            const res = await this.axios.get("http://localhost:3000/students");
            this.asignado =  res.data[0].assignedExercise;
            console.log("estudiantes",res.data)
        },
  },
};
</script>

<style>
p {
  color: aliceblue;
  text-align: center;
  font-size: 250%;
  padding: 50px;
}
</style>
