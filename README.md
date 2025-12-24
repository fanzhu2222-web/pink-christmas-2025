<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Pink Christmas Tree 2025</title>
<style>
  body {
    margin: 0;
    background: #FFF0F5;
    overflow: hidden;
    font-family: Arial, sans-serif;
  }
  canvas {
    display: block;
    margin: auto;
  }
  #musicBtn {
    position: fixed;
    bottom: 20px;
    right: 20px;
    background: #FF69B4;
    color: white;
    border: none;
    border-radius: 50px;
    padding: 12px 18px;
    font-size: 14px;
  }
</style>
</head>

<body>
<canvas id="c" width="360" height="640"></canvas>

<button id="musicBtn">🎵 Play Music</button>

<audio id="bgm" loop>
  <source src="https://cdn.pixabay.com/audio/2022/12/02/audio_8d6c7fd62d.mp3" type="audio/mpeg">
</audio>

<script>
const canvas = document.getElementById("c");
const ctx = canvas.getContext("2d");

// 适配手机屏幕
canvas.width = window.innerWidth;
canvas.height = window.innerHeight;

// 雪花
let snowflakes = [];
for (let i = 0; i < 80; i++) {
  snowflakes.push({
    x: Math.random() * canvas.width,
    y: Math.random() * canvas.height,
    r: Math.random() * 3 + 1,
    d: Math.random() + 1
  });
}

function drawSnow() {
  ctx.fillStyle = "white";
  snowflakes.forEach(s => {
    ctx.beginPath();
    ctx.arc(s.x, s.y, s.r, 0, Math.PI * 2);
    ctx.fill();
  });
}

function updateSnow() {
  snowflakes.forEach(s => {
    s.y += s.d;
    if (s.y > canvas.height) {
      s.y = 0;
      s.x = Math.random() * canvas.width;
    }
  });
}

// 画树
function drawTree() {
  // 树干
  ctx.fillStyle = "#D2B48C";
  ctx.fillRect(canvas.width/2 - 20, canvas.height - 180, 40, 60);

  const layers = [
    { y: canvas.height - 200, w: 160, c: "#FFB6C1" },
    { y: canvas.height - 260, w: 120, c: "#FF69B4" },
    { y: canvas.height - 320, w: 80, c: "#FF1493" }
  ];

  layers.forEach(l => {
    ctx.beginPath();
    ctx.moveTo(canvas.width/2 - l.w, l.y);
    ctx.lineTo(canvas.width/2 + l.w, l.y);
    ctx.lineTo(canvas.width/2, l.y - 180);
    ctx.closePath();
    ctx.fillStyle = l.c;
    ctx.fill();
  });
}

// 星星
function drawStar(cx, cy) {
  ctx.fillStyle = "#FFD700";
  ctx.beginPath();
  for (let i = 0; i < 5; i++) {
    ctx.lineTo(
      cx + Math.cos((18 + i * 72) * Math.PI / 180) * 25,
      cy - Math.sin((18 + i * 72) * Math.PI / 180) * 25
    );
    ctx.lineTo(
      cx + Math.cos((54 + i * 72) * Math.PI / 180) * 10,
      cy - Math.sin((54 + i * 72) * Math.PI / 180) * 10
    );
  }
  ctx.closePath();
  ctx.fill();
}

// 爱心（闪烁）
let pulse = 0;
function drawHeart(x, y, s, color) {
  ctx.fillStyle = color;
  ctx.beginPath();
  ctx.moveTo(x, y);
  ctx.bezierCurveTo(x - s, y - s, x - s * 2, y + s, x, y + s * 2);
  ctx.bezierCurveTo(x + s * 2, y + s, x + s, y - s, x, y);
  ctx.fill();
}

function animate() {
  ctx.clearRect(0, 0, canvas.width, canvas.height);
  drawSnow();
  updateSnow();
  drawTree();
  drawStar(canvas.width/2, canvas.height - 370);

  pulse = Math.sin(Date.now() / 300) * 2;
  drawHeart(canvas.width/2 - 60, canvas.height - 260, 12 + pulse, "#FF1493");
  drawHeart(canvas.width/2 + 50, canvas.height - 220, 10 + pulse, "#FFFFFF");
  drawHeart(canvas.width/2 - 80, canvas.height - 200, 14 + pulse, "#FFB6C1");

  ctx.fillStyle = "#DB7093";
  ctx.font = "bold 22px Arial";
  ctx.textAlign = "center";
  ctx.fillText("Merry Christmas 2025", canvas.width/2, canvas.height - 40);

  requestAnimationFrame(animate);
}
animate();

// 音乐按钮
const music = document.getElementById("bgm");
document.getElementById("musicBtn").onclick = () => {
  music.play();
};
</script>
</body>
</html>
