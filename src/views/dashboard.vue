<template>
  <div id="app">
    <div>
      <Stepper></Stepper>
    </div>
    <main class="flexbox">
      <!-- <Board id="board-1">
        <Card id="card-1" draggable="true">
          <p>Card one</p>
        </Card>
      </Board>

      <Board id="board-2">
        <Card id="card-2" draggable="true">
          <p>Card two</p>
        </Card>
      </Board> -->
      <v-row>
        <v-col class="">
          <Board2 id="board-1"> </Board2>
        </v-col>

        <v-col>
          <Board2 id="board-2">
            <v-row>
              <v-col cols="6" md="6">
                <!-- <Card2 id="card-1" draggable="true">
                <v-img
                  src="../assets/manzana.png"
                  class="white--text align-end"
                  gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)"
                  width="200" 
                  height="100"
                >
                </v-img>
              </Card2> -->
                <Card2 id="card-1" draggable="true">
                  <h1>1</h1>
                </Card2>
                <Card2 id="card-2" draggable="true">
                  <h1>1/2</h1>
                </Card2>
              </v-col>

              <v-col cols="6" md="6">
                <Card2 id="card-3" draggable="true">
                  <h1>1/4</h1>
                </Card2>
                <Card2 id="card-4" draggable="true">
                  <h1>2</h1>
                </Card2>
               
              </v-col>
            </v-row>
          </Board2>
        </v-col>
      </v-row>
    </main>
  </div>
</template>

<script>
// @ is an alias to /src
import Card from "@/components/Card.vue";
import Board from "../components/Board.vue";
import pizza from "../components/pizza.vue";
import Board2 from "../components/Board2.vue";
import Card2 from "../components/Card2.vue";
import Stepper from "../components/Stepper.vue";

export default {
  name: "dashboard",
  components: {
    Card,
    Board,
    pizza,
    Board2,
    Card2,
    Stepper,
  },

  data: () => ({
    cards: [
      { title: "Pre-fab homes", src: "pizarra.jpg", flex: 12 },
      {
        title: "Favorite road trips",
        src: "https://cdn.vuetifyjs.com/images/cards/road.jpg",
        flex: 6,
      },
      {
        title: "Best airlines",
        src: "https://cdn.vuetifyjs.com/images/cards/plane.jpg",
        flex: 6,
      },
    ],
  }),
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.body {
  background-color: bisque;
}

.flexbox {
  display: flex;
  justify-content: space-between;

  width: 100%;
  max-width: 90%;
  height: 100vh;

  overflow: hidden;

  margin: 0 auto;
  padding: 15px;
}

.flexbox .board {
  display: flex;
  flex-direction: column;
  height: 50%;
  max-width: 100%;
  background-color: rgb(63, 63, 63);
  padding: 15px;
}

.flexbox .board .card {
  padding: 15px 25px;
  max-width: 100%;
  background-color: azure;
  cursor: pointer;
  margin-bottom: 15px;
}
</style>
