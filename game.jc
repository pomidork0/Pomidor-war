const canvas = document.getElementById('game');
const ctx = canvas.getContext('2d');

const tomato = {
  x: 50,
  y: 300,
  w: 40,
  h: 40,
  vx: 0,
  vy: 0,
  onGround: false,
};

const gravity = 0.5;
const groundY = 350;
let keys = {};
let enemies = [];

function drawTomato() {
  ctx.fillStyle = 'red';
  ctx.beginPath();
  ctx.ellipse(tomato.x + tomato.w / 2, tomato.y + tomato.h / 2, 20, 20, 0, 0, Math.PI * 2);
  ctx.fill();
}

function drawGround() {
  ctx.fillStyle = 'green';
  ctx.fillRect(0, groundY, canvas.width, canvas.height - groundY);
}

function spawnRat() {
  enemies.push({ x: canvas.width, y: groundY - 30, w: 30, h: 30, vx: -2 });
}

function drawEnemies() {
  ctx.fillStyle = 'gray';
  enemies.forEach(r => {
    ctx.fillRect(r.x, r.y, r.w, r.h);
    r.x += r.vx;
  });
}

function updateTomato() {
  tomato.vy += gravity;
  tomato.y += tomato.vy;

  if (keys['ArrowRight']) tomato.vx = 3;
  else if (keys['ArrowLeft']) tomato.vx = -3;
  else tomato.vx = 0;

  tomato.x += tomato.vx;

  if (tomato.y + tomato.h >= groundY) {
    tomato.y = groundY - tomato.h;
    tomato.vy = 0;
    tomato.onGround = true;
  } else {
    tomato.onGround = false;
  }
}

function gameLoop() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  drawGround();
  updateTomato();
  drawTomato();
  drawEnemies();
  requestAnimationFrame(gameLoop);
}

setInterval(spawnRat, 2000);
gameLoop();

window.addEventListener('keydown', e => {
  keys[e.key] = true;
  if (e.key === ' ' && tomato.onGround) {
    tomato.vy = -10;
  }
});

window.addEventListener('keyup', e => {
  keys[e.key] = false;
});
