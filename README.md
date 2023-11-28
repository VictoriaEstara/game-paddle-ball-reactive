## Gambaran Umum
Kode ini merupakan permainan sederhana berupa paddle ball yang telah menerapkan Paradigma Reactive Programming. Paddle ball adalah permainan yang menyuruh player atau pengguna untuk menahan ball menggunakan paddle. Paddle dapat digerakkan ke atas menggunakan tombol 'arrow-up' pada keyboard dan ke bawah menggunakan tombol 'arrow-down' pada keyboard.

## Bahasa Pemrograman
Kode proyek ini ditulis menggunakan bahasa pemrograman JavaScript dengan framework vue.js.

## Software Pendukung
Proyek ini dikembangkan menggunakan [Visual Studio Code](https://code.visualstudio.com/download) dengan memasang [Node.js](https://nodejs.org) V12+. Pastikan Anda memiliki kedua hal tersebut sebelum menjalankan proyek.

## Cara Penggunaan
Buka proyek menggunakan Visual Studio Code atau coba bermain melalui [tautan](https://play.vuejs.org/#eNqdV9ty2zYQ/ZUN08Rua92iSaZVJE+dxtNxJ9N46vZND4HJFQULvAwA6jKO/r0LQCRBmpLTPIncXZxdnD0AV4/BVZ731wUGk2CqMckF03g5TwGmEV8Dj2bzgOX5PCCbsZL9Ra8HNymHVRYh7FgaQ4JpzHQhQSILNV8j9HoW44Cy7vEF4byIWYJ3mkmNkQd4BDLhYdEBSNH3hdZZCr+FgocrwlUG8g/CJlALD+ZlOnBxZSEDqqRZFArltlrZQsGUIkRTaC/MUs14itLW6qJacTmLIkFpYaL0TiBZHkFn+QS+/PBITO5Q3maKa56l+1dfYE9AfhlP4O6ZEN1gxlNC9XcEdgECF/qpb9udqPXmNcVs9fO6vck2xRJ9kv92b100t4iunsun6cATGb2qUPJc0zNu84wgI1ywQmh4NIsiptn5j+4ZSAsksbR8A/DUNIEFo2Ze+C6zqba92ZMJvB1WLp/FCTzC1nphZ35g3wi7y9GktDEjGzKqIvbvza97S1Avs0hRpPNVFNZ7AtBLrvreVmAGWhZoYRp+sx9y2g01vdQcPOA2HSzlCTFdmcsivW4+KeWbwU6X5qUq4VqJmr2g5W+HTWS/I+Rut+RpsO1LGVk1plVQkq3x1qY+xzWm2iuLL+C8sSfPV8rvPQwGYO46lsI9ZxLcFUCKgxglW4FiTFv9ASWS5fJ9fdnZrP1c2t+PTu6WVL8MF7TCHcxmMzi7kjLb/JufwevXneRdwrBRa1dMbwajmuE9mNvvaK6P2SY9mm0Kvz6f7udmumYTKi3VKHTbKg081SjXTNyYPpJybg7v5xQ6u/Rznm4W4Qlkslpe49byrUhorLOYRiQfSFGe2Ks9mF3A6F37TNVLWjpvXs+Gl6Zg+9vjsu/vOuJ3nlZIjFdOjM0PMX0+WaoLsTIyzQSDIqfbNIWI+vpE7q2Ml9Re+Pq1s5ppl9C80uCnGfRGftv/d6URP5wpv86OjB6n0xm8IbGeCqJtHYhs6fS5ZYTdKW8YD8uFpxjZfgsjRU0JUSHr6wMe+Io5WhIUuGG6i5xOSroa5d3VjW9Ms6hPWcxDKKiSVXd3eBrHnG4+lAnNR+wZQW2NoH7pFtSROk/SVx+6w1c2o1Ixqs/dhqck8z7RdG1utk9caaQp7vyMrjij/7OL+pC7L4E7ywbOfC2mg2ooMQOKmcXo8SVNwYephCsjBpotBLqzywSP0x6nyYY+9iHlRGntD4XSfLGzkyRZG74l8nhJptFwuF6SxfbAdqgePF2+vJpKJNLgRNOwBdjwSC8nJMNh7qooEd9UlnsWrmJJ/ESEKTIah14iutVGXQuRbSaw5FGEaVXB4XvWyszuVSYK3cg8aid+dyLveDyuUpj2fleCynA0AbkyGaHsSRbxgrrxdvjK5aWu2k4GF4FWxPCCx/0HlaX0v8eWMg/CLMm5QPk5NyWpeVANbvQXSBBXf1qbOTmHO5/WLDFcddgf1NbY5sGtGYDkmqbmykejV4zaua/v/sItPVfOJIsK84/ihJOmb0MV1ejCPhANVLYXZ6u9ScxATWf1H3W9JfmpclOm0Pr4zAP68/f7ia3X5Y77Y7uO+Az2/wHiyIDy) ini secara online.

note: Jika anda menggunakan Visual Studi Code, masukkan kode berikut ke dalam terminal untuk menginstall 'npm' dan menampilkan tautan local/host/
```sh
npm install
npm run dev
```

## Contoh Penggunaan Program

```vue
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
