# 猜数字游戏



## 说明

经典的猜数字游戏。系统随机生成 1-100 之间的数字，玩家每次输入后获得"大了"或"小了"的提示。



## 代码

```html

<!DOCTYPE html>

<html lang="zh">

<head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1">

<title>猜数字</title>

<style>

body{font-family:Arial;text-align:center;margin:40px;background:linear-gradient(135deg,#667eea,#764ba2);color:white;min-height:100vh}

.card{background:rgba(255,255,255,0.15);padding:30px;border-radius:16px;max-width:350px;margin:0 auto;backdrop-filter:blur(10px)}

input{width:80px;font-size:32px;text-align:center;padding:8px;border:none;border-radius:8px;margin:10px}

button{font-size:18px;padding:10px 25px;border:none;border-radius:8px;background:#ff9800;color:white;cursor:pointer;margin:5px}

#hint{font-size:22px;min-height:40px;margin:15px 0}

#history{color:rgba(255,255,255,0.7);max-height:100px;overflow-y:auto}

</style></head>

<body>

<div class="card">

<h2>🎯 猜数字</h2><p>1 ~ 100</p>

<input type="number" id="guess" min="1" max="100" placeholder="?">

<button onclick="checkGuess()">猜!</button>

<div id="hint"></div><div id="history"></div>

<button onclick="newGame()" style="background:#4CAF50">新游戏</button>

</div>

<script>

let target = Math.floor(Math.random()*100)+1;

let attempts = 0, history = [];



function checkGuess() {

  let guess = parseInt(document.getElementById("guess").value);

  if (isNaN(guess) || guess<1 || guess>100) { alert("请输入1~100的数字"); return; }

  attempts++; history.push(guess);

  document.getElementById("history").textContent = "已猜: "+history.join(", ");

  let h = document.getElementById("hint");

  if (guess === target) {

    h.textContent = "🎉 正确! 共猜了"+attempts+"次";

    if(attempts<=5) h.textContent+=" 天才!";

    else if(attempts<=10) h.textContent+=" 不错!";

  } else if (guess > target) h.textContent = "📉 大了!";

  else h.textContent = "📈 小了!";

}

function newGame() {

  target = Math.floor(Math.random()*100)+1; attempts = 0; history = [];

  document.getElementById("hint").textContent=""; document.getElementById("history").textContent="";

  document.getElementById("guess").value="";

}

</script></body></html>

```

