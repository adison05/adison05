<!DOCTYPE html>
<html lang="pl">
<head>
  <meta charset="UTF-8">
  <title>Gra Snake</title>
  <style>
    canvas { background-color: black; display: block; margin: auto; }
  </style>
</head>
<body>
  <canvas id="game" width="400" height="400"></canvas>
  <script>
    const canvas = document.getElementById('game');
    const ctx = canvas.getContext('2d');
    let snake = [{ x: 200, y: 200 }];
    let direction = 'RIGHT';
    let food = { x: 100, y: 100 };

    document.addEventListener('keydown', changeDirection);

    function changeDirection(e) {
      if (e.key === 'ArrowUp' && direction !== 'DOWN') direction = 'UP';
      if (e.key === 'ArrowDown' && direction !== 'UP') direction = 'DOWN';
      if (e.key === 'ArrowLeft' && direction !== 'RIGHT') direction = 'LEFT';
      if (e.key === 'ArrowRight' && direction !== 'LEFT') direction = 'RIGHT';
    }

    function drawSnake() {
      ctx.fillStyle = 'lime';
      snake.forEach(part => ctx.fillRect(part.x, part.y, 20, 20));
    }

    function moveSnake() {
      let head = { ...snake[0] };
      if (direction === 'UP') head.y -= 20;
      if (direction === 'DOWN') head.y += 20;
      if (direction === 'LEFT') head.x -= 20;
      if (direction === 'RIGHT') head.x += 20;
      snake.unshift(head);
      if (head.x === food.x && head.y === food.y) {
        spawnFood();
      } else {
        snake.pop();
      }
    }

    function spawnFood() {
      food.x = Math.floor(Math.random() * 20) * 20;
      food.y = Math.floor(Math.random() * 20) * 20;
    }

    function drawFood() {
      ctx.fillStyle = 'red';
      ctx.fillRect(food.x, food.y, 20, 20);
    }

    function gameLoop() {
      ctx.clearRect(0, 0, canvas.width, canvas.height);
      drawFood();
      drawSnake();
      moveSnake();
      if (snake[0].x < 0 || snake[0].x >= canvas.width || snake[0].y < 0 || snake[0].y >= canvas.height) {
        alert('Game Over');
        snake = [{ x: 200, y: 200 }];
        direction = 'RIGHT';
      }
      setTimeout(gameLoop, 100);
    }

    spawnFood();
    gameLoop();
  </script>
</body>
</html>



<!---
adison05/adison05 is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->
