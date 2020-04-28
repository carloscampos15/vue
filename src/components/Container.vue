<template>
  <div>
    <v-app-bar app color="blue darken-4" dark>
      <v-container class="fill-height">
        <v-toolbar-title>CAMPOS INC</v-toolbar-title>
      </v-container>
    </v-app-bar>

    <v-content>
      <v-container class="fill-height">
        <v-row
          v-for="(comentario, index) of comentarios"
          v-bind:key="index"
          align="center"
          justify="center"
        >
          <v-col>
            <v-card class="mx-auto" elevation="5" :color="comentario.color" outlined>
              <v-card-text class="white--text">{{comentario.nombre}}</v-card-text>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-content>

    <v-dialog v-model="dialog" width="700">
      <template v-slot:activator="{ on }">
        <v-btn v-on="on" fab dark large color="primary" fixed right bottom>
          <v-icon>mdi-plus</v-icon>
        </v-btn>
      </template>
      <v-card>
        <v-card-text style="padding-bottom: 0">
          <br />
          <v-textarea v-model="nuevoComentario" outlined label="Comentario"></v-textarea>
        </v-card-text>
        <v-divider></v-divider>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="success" text @click="agregarComentario">ENVIAR</v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/database";

const db = firebase
  .initializeApp({ databaseURL: "https://habilidades-94935.firebaseio.com/" })
  .database();

export default {
  props: {
    source: String
  },
  data: () => ({
    dialog: false,
    nuevoComentario: "",
    comentarios: []
  }),
  methods: {
    agregarComentario() {
      if (this.nuevoComentario === "") return;

      let colores = [
        "pink",
        "indigo",
        "blue",
        "teal",
        "green",
        "orange",
        "grey",
        "deep-orange",
        "brown",
        "blue-grey",
        "yellow darken-3",
        "green accent-3"
      ];

      let color = colores[Math.floor(Math.random() * colores.length)];

      db.ref('comentarios').push({
        nombre: this.nuevoComentario,
        color: color
      })

      // this.comentarios.push({
      //   nombre: this.nuevoComentario,
      //   color: color
      // });

      this.nuevoComentario = "";
      this.dialog = false;
    }
  },
  firebase: {
    comentarios: db.ref("comentarios")
  }
};
</script>