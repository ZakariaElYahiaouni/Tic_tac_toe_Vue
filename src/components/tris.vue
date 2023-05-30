<template>
  <h1>{{ title }}</h1>
  <br />
  <div id="main-container">
    <div id="0-0" class="container" @click="eventFunction($event, '0-0')"></div>
    <div id="0-1" class="container" @click="eventFunction($event, '0-1')"></div>
    <div id="0-2" class="container" @click="eventFunction($event, '0-2')"></div>
    <div id="1-0" class="container" @click="eventFunction($event, '1-0')"></div>
    <div id="1-1" class="container" @click="eventFunction($event, '1-1')"></div>
    <div id="1-2" class="container" @click="eventFunction($event, '1-2')"></div>
    <div id="2-0" class="container" @click="eventFunction($event, '2-0')"></div>
    <div id="2-1" class="container" @click="eventFunction($event, '2-1')"></div>
    <div id="2-2" class="container" @click="eventFunction($event, '2-2')"></div>
  </div>
</template>

<script>
export default {
  name: "trisGenerate",
  props: {
    title: String,
  },
  data() {
    return {
      flag: true,
      mapGame: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
    };
  },
  methods: {
    eventFunction: function (event, id) {
      if (document.getElementById(id).innerHTML === "") {
        // divide l'id del container in due numeri s che rappresentano la riga e la colonna
        const [row, col] = id.split("-").map((i) => parseInt(i));

        // aggiorna il valore della matrice nella posizione corrispondente
        if (this.flag === true) {
          document.getElementById(id).innerHTML = "X";
          this.mapGame[row][col] = "X";
          console.log(this.mapGame);
          this.checkWin();
          this.flag = false;
        } else if (this.flag === false) {
          document.getElementById(id).innerHTML = "O";
          this.mapGame[row][col] = "O";
          this.flag = true;
          console.log(this.mapGame);
          this.checkWin();
        }
      }
    },
    isMatrixFull: function () {
      for (let i = 0; i < this.mapGame.length; i++) {
        for (let j = 0; j < this.mapGame[i].length; j++) {
          if (this.mapGame[i][j] === "") {
            return false;
          }
        }
      }
      return true;
    },
    checkWin: function () {
      // Verifica le righe della matrice
      for (let i = 0; i < 3; i++) {
        if (
          this.mapGame[i][0] !== "" &&
          this.mapGame[i][0] === this.mapGame[i][1] &&
          this.mapGame[i][1] === this.mapGame[i][2]
        ) {
          alert("Player " + this.mapGame[i][0] + " won");
          this.resetGame();
        }
      }

      // Verifica le colonne della matrice
      for (let j = 0; j < 3; j++) {
        if (
          this.mapGame[0][j] !== "" &&
          this.mapGame[0][j] === this.mapGame[1][j] &&
          this.mapGame[1][j] === this.mapGame[2][j]
        ) {
          alert("Player " + this.mapGame[0][j] + " won");
          this.resetGame();
        }
      }

      // Verifica la prima diagonale della matrice
      if (
        this.mapGame[0][0] !== "" &&
        this.mapGame[0][0] === this.mapGame[1][1] &&
        this.mapGame[1][1] === this.mapGame[2][2]
      ) {
        alert("Player " + this.mapGame[0][0] + " won");
        this.resetGame();
      }

      // Verifica la seconda diagonale della matrice
      if (
        this.mapGame[0][2] !== "" &&
        this.mapGame[0][2] === this.mapGame[1][1] &&
        this.mapGame[1][1] === this.mapGame[2][0]
      ) {
        alert("Player " + this.mapGame[0][2] + " won");
        this.resetGame();
      }
      if (this.isMatrixFull()) {
        alert("draw");
        this.resetGame();
      }
    },
    resetGame: function () {
      for (let i = 0; i < 3; i++) {
        for (let j = 0; j < 3; j++) {
          this.mapGame[i][j] = "";
          document.getElementById(i + "-" + j).innerHTML = "";
        }
      }
    },
  },
};
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#main-container {
  display: grid;
  grid-template-columns: auto auto auto;
  padding: 15px;
  width: 610px;
  margin: auto;
}
.container {
  background-color: bisque;
  border: 1px solid black;
  padding: 20px;
  font-size: 30px;
  text-align: center;
  width: 200px;
  height: 200px;
  cursor: pointer;
  transition: 200ms;
}
.container:hover {
  background-color: orange;
  color: white;
}
</style>
