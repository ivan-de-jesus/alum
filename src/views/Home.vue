<template>
<div  id="building" class="home">
   <v-alert color="red" border="left"  icon="$mdiAccount" type="warning" :value="alert"></v-alert>

    <v-content>
        <v-container fluid fill-height>
            <v-layout align-center justify-center>
                <v-flex xs12 sm8 md4>
                    <v-card class="elevation-12">
                        <v-toolbar dark color="primary">
                            <v-toolbar-title>Iniciar secion</v-toolbar-title>
                        </v-toolbar>
                        <v-card-text>
                            <v-form>
                                <v-text-field name="login" label="Nombre completo" type="text" v-model="name"></v-text-field>
                                <v-text-field id="password" name="password" label="Contraseña" type="password" v-model="pass">
                                    <v-icon>fas fa-lock</v-icon>
                                </v-text-field>
                            </v-form>
                        </v-card-text>
                        <v-card-actions>
                            <v-spacer></v-spacer>
                            <v-btn @click="validation" color="primary" to="/">Entrar</v-btn>
                        </v-card-actions>
                    </v-card>
                </v-flex>
            </v-layout>
        </v-container>
    </v-content>
</div>
</template>

<script>
// @ is an alias to /src

export default {
    name: "Home",
    props: {
        source: String,
    },
    components: {},
    data: () => ({
        name: "",
        pass: "",
        students: [],
        alert: false,
    }),
    created() {
        this.getStudents();
    },

    methods: {
        
        async getStudents() {
            const res = await this.axios.get("http://localhost:3000/students");
            this.students = res.data;
        },
        validation() {

            for (let i = 0; i < this.students.length; i++) {
                if (this.name === this.students[i].name && this.pass === this.students[i].pass) {
                    this.$router.push("Dashboard");
                } else {
                  this.alert = true;
                }
            }
        },
    },
};
</script>

<style>
#building{
background:url("../assets/fondo.png");
width:100%;		
height:100%;		
position:fixed;
background-size:100% 100%;
}
</style>