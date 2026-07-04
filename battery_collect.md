# 电池收集游戏



## 说明

用方向键或 WASD 控制机器人收集散落在画面中的电池，躲避障碍。



## 代码

```html

<!DOCTYPE html>

<html lang="zh">

<head><meta charset="UTF-8"><title>收集电池</title>

<style>

body{text-align:center;font-family:Arial;margin:10px;background:#111;color:white}

canvas{background:#1a1a1a;border:2px solid #4caf50}

</style></head>

<body>

<h2>🔋 收集电池</h2><div id="hud">🔋 <span id="bat">0</span></div>

<canvas id="c" width="500" height="400"></canvas>

<script>

const ctx=document.getElementById("c").getContext("2d");

let player={x:250,y:200,r:15},bats=[],obs=[],collected=0;



for(let i=0;i<8;i++)bats.push({x:Math.random()*480,y:Math.random()*380});

for(let i=0;i<5;i++)obs.push({x:Math.random()*480,y:Math.random()*380,r:20});



let keys={};

document.addEventListener("keydown",e=>keys[e.key]=true);

document.addEventListener("keyup",e=>keys[e.key]=false);



function loop(){

  if(keys["ArrowUp"]||keys["w"])player.y-=3;

  if(keys["ArrowDown"]||keys["s"])player.y+=3;

  if(keys["ArrowLeft"]||keys["a"])player.x-=3;

  if(keys["ArrowRight"]||keys["d"])player.x+=3;

  player.x=Math.max(15,Math.min(485,player.x));player.y=Math.max(15,Math.min(385,player.y));



  // 碰撞检测

  bats=bats.filter(b=>{

    let d=Math.hypot(player.x-b.x,player.y-b.y);

    if(d<player.r+8){collected++;document.getElementById("bat").textContent=collected;bats.push({x:Math.random()*480,y:Math.random()*380});return false;}return true;

  });

  for(let o of obs){if(Math.hypot(player.x-o.x,player.y-o.y)<player.r+o.r){alert("💥 Game Over! 收集到 "+collected+" 个电池");location.reload();}}



  ctx.clearRect(0,0,500,400);

  ctx.beginPath();ctx.arc(player.x,player.y,player.r,0,Math.PI*2);ctx.fillStyle="#ff9800";ctx.fill();

  bats.forEach(b=>{ctx.beginPath();ctx.arc(b.x,b.y,8,0,Math.PI*2);ctx.fillStyle="#4caf50";ctx.fill();ctx.fillStyle="white";ctx.font="10px Arial";ctx.fillText("🔋",b.x-6,b.y+4);});

  obs.forEach(o=>{ctx.beginPath();ctx.arc(o.x,o.y,o.r,0,Math.PI*2);ctx.fillStyle="#f44336";ctx.fill();});

  requestAnimationFrame(loop);

}

loop();

</script></body></html>

```

