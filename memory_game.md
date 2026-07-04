# 记忆配对游戏



## 说明

翻牌配对。点击卡片翻转，找到相同的两张配对即为成功。训练记忆力。



## 代码

```html

<!DOCTYPE html>

<html lang="zh">

<head><meta charset="UTF-8"><title>记忆配对</title>

<style>

body{text-align:center;font-family:Arial;margin:20px;background:#f3e5f5}

.grid{display:grid;grid-template-columns:repeat(4,80px);gap:10px;justify-content:center}

.card{width:80px;height:80px;background:#7b1fa2;color:white;font-size:36px;display:flex;align-items:center;justify-content:center;border-radius:10px;cursor:pointer}

.card.flipped,.card.matched{background:white;color:#333;border:2px solid #7b1fa2}

#score{font-size:20px;margin:10px;color:#7b1fa2}

</style></head>

<body>

<h2>🧠 记忆配对</h2><div id="score">步数: 0</div>

<div class="grid" id="grid"></div><button onclick="reset()" style="margin:15px;padding:10px 25px;background:#7b1fa2;color:white;border:none;border-radius:8px;cursor:pointer;font-size:16px">新游戏</button>



<script>

const emojis=["🍎","🍊","🍋","🍇","🌸","🌻","🎸","🎹"],cards=[...emojis,...emojis];let flipped=[],matched=new Set(),steps=0,locked=false;



function shuffle(a){for(let i=a.length-1;i>0;i--){let j=Math.floor(Math.random()*(i+1));[a[i],a[j]]=[a[j],a[i]]}}



function render(){

  let g=document.getElementById("grid");g.innerHTML="";

  cards.forEach((c,i)=>{

    let d=document.createElement("div");d.className="card";d.textContent=flipped.includes(i)||matched.has(i)?c:"?";

    if(flipped.includes(i)||matched.has(i))d.classList.add("flipped");if(matched.has(i))d.classList.add("matched");

    d.addEventListener("click",()=>flip(i));g.appendChild(d);

  });

}

function flip(i){

  if(locked||flipped.includes(i)||matched.has(i))return;

  flipped.push(i);render();

  if(flipped.length===2){

    steps++;document.getElementById("score").textContent="步数: "+steps;

    let[a,b]=flipped;

    if(cards[a]===cards[b]){matched.add(a);matched.add(b);flipped=[];render();if(matched.size===16)setTimeout(()=>alert("🎉 完成! 用了"+steps+"步"),300);}

    else{locked=true;setTimeout(()=>{flipped=[];locked=false;render();},800);}

  }

}

function reset(){shuffle(cards);flipped=[];matched.clear();steps=0;locked=false;document.getElementById("score").textContent="步数: 0";render();}

shuffle(cards);render();

</script></body></html>

```

