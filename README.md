<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Kashmir Game – Colour Trading</title>

<style>
body{
    margin:0;
    font-family: Arial, sans-serif;
    background: linear-gradient(135deg,#0f2027,#203a43,#2c5364);
    color:#fff;
}
.header{
    background:#0b3d91;
    padding:15px;
    text-align:center;
    font-size:22px;
    font-weight:bold;
}
.container{
    max-width:420px;
    margin:auto;
    padding:15px;
}
.box{
    background:#12263a;
    padding:12px;
    border-radius:10px;
    margin-bottom:12px;
    display:flex;
    justify-content:space-between;
}
.timer{
    text-align:center;
    font-size:20px;
    margin:15px 0;
}
.colors{
    display:grid;
    grid-template-columns:repeat(3,1fr);
    gap:12px;
}
.color{
    padding:25px 0;
    border-radius:12px;
    text-align:center;
    font-weight:bold;
    font-size:18px;
    cursor:pointer;
}
.red{background:#e63946;}
.green{background:#2ecc71;}
.violet{background:#9b59b6;}

.selected{
    outline:3px solid #fff;
}
.result{
    margin-top:15px;
    background:#1b3a4b;
    padding:15px;
    border-radius:10px;
    text-align:center;
    font-size:17px;
}
.footer{
    text-align:center;
    font-size:12px;
    opacity:.7;
    margin-top:20px;
}
</style>
</head>

<body>

<div class="header">KASHMIR GAME</div>

<div class="container">

<div class="box">
    <div>Score: <span id="score">0</span></div>
    <div>Round: <span id="round">1</span></div>
</div>

<div class="timer">
    ⏱ Time Left: <span id="time">30</span>s
</div>

<div class="colors">
    <div class="color red" onclick="selectColor('RED',this)">RED</div>
    <div class="color green" onclick="selectColor('GREEN',this)">GREEN</div>
    <div class="color violet" onclick="selectColor('VIOLET',this)">VIOLET</div>
</div>

<div class="result" id="result">
    Select a colour to start
</div>

<div class="footer">
    Skill Based Game • Kashmir Game
</div>

</div>

<script>
let userChoice = "";
let score = 0;
let time = 30;
let round = 1;
const colors = ["RED","GREEN","VIOLET"];
const timeEl = document.getElementById("time");

function selectColor(color,el){
    userChoice = color;
    document.querySelectorAll(".color").forEach(c=>c.classList.remove("selected"));
    el.classList.add("selected");
}

function generateResult(){
    const result = colors[Math.floor(Math.random()*colors.length)];
    if(userChoice === result){
        score += 10;
        document.getElementById("result").innerHTML =
            "🎉 You Win!<br>Result: <b>"+result+"</b>";
    }else{
        document.getElementById("result").innerHTML =
            "❌ Try Again<br>Result: <b>"+result+"</b>";
    }
    document.getElementById("score").innerText = score;
    round++;
    document.getElementById("round").innerText = round;
    userChoice="";
    document.querySelectorAll(".color").forEach(c=>c.classList.remove("selected"));
}

setInterval(()=>{
    time--;
    timeEl.innerText = time;
    if(time === 0){
        generateResult();
        time = 30;
    }
},1000);
</script>

</body>
</html>
