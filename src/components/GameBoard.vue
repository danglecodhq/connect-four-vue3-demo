<script lang="ts">
import { defineComponent, reactive, ref } from "vue";
import GameCell from "./GameCell.vue";

type Player = "red" | "yellow" | "blue";

export default defineComponent({
  name: "GameBoard",
  components: {
    GameCell,
  },
  setup() {
    const ROWS = 6;
    const COLS = 7;

    const players: Player[] = ["red", "yellow", "blue"];
    const board = reactive<(Player | null)[][]>(
      Array.from({ length: ROWS }, () => Array(COLS).fill(null))
    );

    const currentPlayerIndex = ref(0);
    const currentPlayer = ref<Player>(players[currentPlayerIndex.value]);
    const winner = ref<Player | null>(null);

    function dropDisc(col: number) {
      if (winner.value) return;

      for (let row = ROWS - 1; row >= 0; row--) {
        if (!board[row][col]) {

           // Play drop sound
      const audio = new Audio('/player-action-a.mp3');
      audio.play();


          board[row][col] = currentPlayer.value;
          if (checkWinner(row, col)) {
            // Play winner sound
              const audio_winner = new Audio('/reward.mp3');
             audio_winner.play();
             
            winner.value = currentPlayer.value;
          } else {
            currentPlayerIndex.value =
              (currentPlayerIndex.value + 1) % players.length;
            currentPlayer.value = players[currentPlayerIndex.value];
          }
          break;
        }
      }
    }

    function checkWinner(row: number, col: number): boolean {
      const directions = [
        [0, 1],
        [1, 0],
        [1, 1],
        [1, -1],
      ];
      const player = board[row][col];
      if (!player) return false;

      for (const [dr, dc] of directions) {
        let count = 1;

        for (let i = 1; i < 4; i++) {
          const r = row + dr * i;
          const c = col + dc * i;
          if (
            r < 0 ||
            r >= ROWS ||
            c < 0 ||
            c >= COLS ||
            board[r][c] !== player
          )
            break;
          count++;
        }

        for (let i = 1; i < 4; i++) {
          const r = row - dr * i;
          const c = col - dc * i;
          if (
            r < 0 ||
            r >= ROWS ||
            c < 0 ||
            c >= COLS ||
            board[r][c] !== player
          )
            break;
          count++;
        }

        if (count >= 4) return true;
      }

      return false;
    }

    function resetGame() {
      for (let r = 0; r < ROWS; r++) {
        for (let c = 0; c < COLS; c++) {
          board[r][c] = null;
        }
      }
      currentPlayerIndex.value = 0;
      currentPlayer.value = players[0];
      winner.value = null;
    }

    return {
      board,
      currentPlayer,
      winner,
      COLS,
      ROWS,
      dropDisc,
      resetGame,
    };
  },
});
</script>

<template>
  <div class="space-y-4 text-center">
    <div
      class="text-xl font-bold py-2 px-4 rounded shadow inline-block"
      :class="
        winner
          ? winner === 'red'
            ? 'bg-red-500 text-white'
            : winner === 'yellow'
            ? 'bg-yellow-400 text-black'
            : 'bg-blue-500 text-white'
          : currentPlayer === 'red'
          ? 'bg-red-100 text-red-800'
          : currentPlayer === 'yellow'
          ? 'bg-yellow-100 text-yellow-800'
          : 'bg-blue-100 text-blue-800'
      "
    >
      <span v-if="winner">🎉 {{ winner }} wins!</span>
      <span v-else>{{ currentPlayer }}'s turn</span>
    </div>

    <div
      class="bg-blue-100 border-8 border-blue-900 rounded-xl grid grid-rows-6 grid-cols-7 gap-0.5 shadow-lg"
      style="width: fit-content; margin: 0 auto;"
    >
      <div
        v-for="rowIndex in ROWS"
        :key="rowIndex"
        style="display: contents"
      >
        <div
          v-for="colIndex in COLS"
          :key="colIndex"
          class="cursor-pointer"
          @click="dropDisc(colIndex - 1)"
        >
          <GameCell :value="board[rowIndex - 1][colIndex - 1]" />
        </div>
      </div>
    </div>

    <button
      @click="resetGame"
      class="mt-4 px-4 py-2 bg-blue-500 text-black rounded hover:bg-blue-600"
    >
      Restart Game
    </button>

   
  </div>
</template>
