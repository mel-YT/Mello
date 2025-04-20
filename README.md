<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Mini Minecraft</title>
  <style>
    body { margin: 0; background: #87ceeb; }
    canvas { display: block; margin: 0 auto; background: #6b8e23; }
  </style>
</head>
<body>
  <canvas id="gameCanvas" width="600" height="400"></canvas>
  <script>
    const canvas = document.getElementById('gameCanvas');
    const ctx = canvas.getContext('2d');

    const blockSize = 40;
    const rows = canvas.height / blockSize;
    const cols = canvas.width / blockSize;
    const world = [];

    for (let y = 0; y < rows; y++) {
      const row = [];
      for (let x = 0; x < cols; x++) {
        row.push(y > rows / 2 ? 'dirt' : null); // земля ниже середины
      }
      world.push(row);
    }

    function drawWorld() {
      for (let y = 0; y < rows; y++) {
        for (let x = 0; x < cols; x++) {
          if (world[y][x] === 'dirt') {
            ctx.fillStyle = '#8B4513';
            ctx.fillRect(x * blockSize, y * blockSize, blockSize, blockSize);
          } else {
            ctx.clearRect(x * blockSize, y * blockSize, blockSize, blockSize);
          }
        }
      }
    }

    canvas.addEventListener('click', (e) => {
      const x = Math.floor(e.offsetX / blockSize);
      const y = Math.floor(e.offsetY / blockSize);
      if (world[y][x]) {
        world[y][x] = null; // удалить блок
      } else {
        world[y][x] = 'dirt'; // поставить блок
      }
      drawWorld();
    });

    drawWorld();
  </script>
</body>
</html>
