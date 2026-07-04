# 颜色点击挑战



## 说明

屏幕出现随机颜色的方块，在限定时间内点击正确颜色的方块得分，点错扣分。



## 代码

```html

<!DOCTYPE html>

<html lang="zh">

<head><meta charset="UTF-8"><meta name="viewport" content="width=device-width,initial-scale=1">

<title>颜色挑战</title>

<style>

*{margin:0;padding:0;box-sizing:border-box}

body{display:flex;align-items:center;justify-content:center;height:100vh;background:#1a1a2e;font-family:Arial;user-select:none;overflow:hidden}

#game{position:relative;width:100%;height:100%}

.block{position:absolute;border-radius:10px;cursor:pointer;transition:opacity 0.3s}

.block:hover{opacity:0.8}

#target{position:fixed;top:15px;left:50%;transform:translateX(-50%);font-size:24px;color:white;z-index:10}

#stats{position:fixed;bottom:15px;left:50%;transform:translateX(-50%);color:white;font-size:18px;z-index:10;display:flex;gap:30px}

</style></head>

<body>

<div id="target">点击 <span id="targetColor" style="font-weight:bold;font-size:28px"></span> 方块!</div>

<div id="game"></div>

<div id="stats"><span>得分: <b id="score">0</b></span><span>时间: <b id="timer">30</b>s</span></div>



<script>

const colors=["#ff6b6b","#feca57","#48dbfb","#ff9ff3","#54a0ff","#5f27cd","#00d2d3","#1dd1a1","#f368e0"];

let target,score=0,time=30;



function newRound(){

  document.getElementById("game").innerHTML="";

  target=colors[Math.floor(Math.random()*colors.length)];

  document.getElementById("targetColor").textContent=target;

  document.getElementById("targetColor").style.color=target;

  for(let i=0;i<25;i++){

    let c=colors[Math.floor(Math.random()*colors.length)];

    let b=document.createElement("div");

    b.className="block";

    b.style.background=c;

    b.style.width=(40+Math.random()*60)+"px";

    b.style.height=(40+Math.random()*60)+"px";

    b.style.left=Math.random()*90+"%";

    b.style.top=Math.random()*85+"%";

    b.addEventListener("click",()=>{

      if(c===target){score+=10;newRound();}

      else score-=5;

      document.getElementById("score").textContent=score;

    });

    document.getElementById("game").appendChild(b);

  }

}



let timer=setInterval(()=>{

  time--;document.getElementById("timer").textContent=time;

  if(time<=0){clearInterval(timer);alert("⏰ 时间到! 最终得分:"+score);location.reload();}

},1000);



newRound();

</script></body></html>

```

