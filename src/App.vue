<template>
  <div id="app">
    <div class="status">{{ status }}</div>
    <button @click="reset">Reset</button>
    <template v-for="row in 3" :key="row">
      <div class="row">
        <button
          @click="registerMove(row, button)"
          v-for="button in 3"
          :key="button" :disabled="board[row - 1][button - 1]!== '' || winnerFound"
          class="square"
          style="width: 40px; height: 40px"
        >
          {{ board[row - 1][button - 1] }}
        </button>
      </div>
    </template>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      status: "Next player: X",
      currentPlayer: "X",
      marker: null,
      winnerFound: false,
      board: [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ],
    };
  },
  watch: {
    board(oldBoard, newBoard) {
      console.log("oldBoard ", oldBoard);
      console.log("newBoard ", newBoard);
    },
  },
  methods: {
    reset(){
      this.status = "Next player: X";
      this.currentPlayer = "X";
      this.marker = null;
      this.winnerFound = false;
      this.board = [
        ["", "", ""],
        ["", "", ""],
        ["", "", ""],
      ];
      this.$forceUpdate();
    },
    checkWinner(board, player) {
      console.log("checkWinner ", board, player);
      if (
        board[0][0] === player &&
        board[0][1] === player &&
        board[0][2] === player
      ) {
        this.status = "Winner: " + player;
        return true;
      } else if (
        board[1][0] === player &&
        board[1][1] === player &&
        board[1][2] === player
      ) {
        this.status = "Winner: " + player;
        return true;
      } else if (
        board[2][0] === player &&
        board[2][1] === player &&
        board[2][2] === player
      ) {
        this.status = "Winner: " + player;
        return true;
      } else if (
        board[0][0] === player &&
        board[1][0] === player &&
        board[2][0] === player
      ) {
        this.status = "Winner: " + player;
        return true;
      } else if (
        board[0][1] === player &&
        board[1][1] === player &&
        board[2][1] === player
      )  {
        this.status = "Winner: " + player;
        return true;
      } else if (
        board[0][0] === player &&
        board[1][1] === player &&
        board[2][2] === player
      )  {
        this.status = "Winner: " + player;
        return true;
      } else if (
        board[0][2] === player &&
        board[1][1] === player &&
        board[2][0] === player
      )  {
        this.status = "Winner: " + player;
        return true;
      } else {
        return false;
      }
    },
    registerMove(row, button) {
      console.log(row, button);
      console.log("board ", this.board);
      console.log("this#.checkWinner ", this.checkWinner(
          this.board,
          this.currentPlayer));
      if (this.board[row - 1][button - 1] === "")
     {
        this.board[row - 1][button - 1] = this.currentPlayer;
        this.winnerFound = this.checkWinner(
          this.board,
          this.currentPlayer);
        if(!this.winnerFound){
            this.status =
          "Next player:" +
          (this.status.split(":")[1].trim() === "X" ? "O" : "X");
        this.currentPlayer === "X"
          ? (this.currentPlayer = "O")
          : (this.currentPlayer = "X");
          }
      }
      this.$forceUpdate();
    },
  },
};
</script>
