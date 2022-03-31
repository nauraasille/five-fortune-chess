<script setup lang="ts">
import { ref } from "vue";

const X = 5;
const Y = 5;

const chessBoard = ref(
  Array.from({ length: Y }, () => Array.from({ length: X }, () => ""))
);

const phase = ref("start");
const players = ref(["white", "black"]);
const activePlayer = ref("white");

function handleChessClick(x: number, y: number) {
  if (phase.value === "start") {
    chessBoard.value[y][x] = activePlayer.value;
    activePlayer.value === players.value[0]
      ? (activePlayer.value = players.value[1])
      : (activePlayer.value = players.value[0]);
  }
}
</script>

<template>
  <div class="w-screen h-screen flex items-center justify-center">
    <div class="p-10 bg-yellow-800">
      <div v-for="(row, y) in chessBoard" :key="y" class="flex">
        <div
          v-for="(item, x) in row"
          :key="x"
          class="relative w-10 h-10 m-5 rounded-full"
        >
          <div
            class="absolute z-0 top-5 left-5 w-20 h-20 border-black"
            :class="{
              'border-t-2': x < X - 1,
              'border-l-2': y < Y - 1,
            }"
          ></div>
          <div
            class="absolute w-10 h-10 rounded-full cursor-pointer select-none text-4xl text-center"
            @click="handleChessClick(x, y)"
            :class="{
              'white-chess': chessBoard[y][x] === 'white',
              'black-chess': chessBoard[y][x] === 'black',
            }"
          >
            {{
              chessBoard[y][x] === "white"
                ? "🌿"
                : chessBoard[y][x] === "black"
                ? "🪨"
                : ""
            }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
/* .white-chess {
  background: radial-gradient(
    15px 15px at 15px 15px,
    rgb(224, 223, 223),
    #b9b3b3
  );
}
.black-chess {
  background: radial-gradient(10px 10px at 15px 15px, #fff, rgb(0, 0, 0));
} */
</style>
