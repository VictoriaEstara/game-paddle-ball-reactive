<template>
  <div id="app">

    <!-- Ini kode yang mengatur reactive -->
    <div v-if="!gameStarted">

      <!-- Ini kode yang memicu reactive -->
      <button @click="startGame">Start Game</button>
    </div>
    <div v-else>
      <div class="game-container">
        <div class="paddle" :style="{ top: `${playerPosition}%` }"></div>
        <div class="ball" :style="{ top: `${ballPosition.y}%`, left: `${ballPosition.x}%` }"></div>
      </div>
      <div v-if="gameOver">
        <button @click="restartGame">Restart Game</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      gameStarted: false,
      gameOver: false,
      playerPosition: 50,
      ballPosition: { x: 50, y: 50 },
      ballSpeed: { x: 1, y: 1 },
    };
  },
  methods: {
    startGame() {
      this.gameStarted = true;
      this.gameOver = false;
      this.resetGame();
      this.animate();
    },
    restartGame() {
      this.resetGame();
      this.animate();
      this.gameOver = false;
    },
    resetGame() {
      this.playerPosition = 50;
      this.ballPosition = { x: 50, y: 50 };
      this.ballSpeed = { x: 1, y: 1 };
    },
    movePlayer(event) {
      if (this.gameOver) {
        return; // aturan biar paddle ga gerak saat game over
      }

      event.preventDefault();

      if (event.key === 'ArrowUp' && this.playerPosition > 0) {
        this.playerPosition -= 10;
      } else if (event.key === 'ArrowDown' && this.playerPosition < 90) {
        this.playerPosition += 10;
      }
    },
    animate() {
      const intervalId = setInterval(() => {
        if (this.gameOver) {
          clearInterval(intervalId);
        } else {
          this.moveBall();
        }
      }, 16);
    },
    moveBall() {
      this.ballPosition.x += this.ballSpeed.x;
      this.ballPosition.y += this.ballSpeed.y;

      // Aturan yang mengatur memantulkan bola up dan down
      if (this.ballPosition.y > 90 || this.ballPosition.y < 0) {
        this.ballSpeed.y *= -1;
      }

      // Aturan yang mengatur memantulkan bola di paddle
      if (
        this.ballPosition.x <= 2 &&
        this.ballPosition.y >= this.playerPosition &&
        this.ballPosition.y <= this.playerPosition + 30
      ) {
        this.ballSpeed.x *= -1;
      }

      // Aturan uyang mengantur game over jika bola melewati paddle
      if (this.ballPosition.x < 0) {
        this.gameOver = true;
      }

      // Logic untuk memantulkan bola di pinggir permainan
      if (this.ballPosition.x > 98 || this.ballPosition.x < 0) {
        this.ballSpeed.x *= -1;
      }
    },
  },
  mounted() {
    window.addEventListener('keydown', this.movePlayer);
  },
};
</script>

<style>
#app {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
}

.game-container {
  position: relative;
  width: 300px;
  height: 200px;
  background-color: #eee;
  overflow: hidden;
}

.paddle {
  position: absolute;
  width: 10px;
  height: 60px;
  background-color: #333;
}

.ball {
  position: absolute;
  width: 10px;
  height: 10px;
  background-color: #333;
  border-radius: 50%;
}
</style>