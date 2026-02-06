# html-and-css
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>2026 Pink Canvas</title>

<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:wght@600;700&family=Poppins:wght@300;400&display=swap" rel="stylesheet">

<style>
body{
margin:0;
height:100vh;
background:rgb(234, 114, 114);
display:flex;
justify-content:center;
align-items:center;
overflow:hidden;
font-family:Poppins;
}

canvas{
border-radius:30px;
box-shadow:
0 0 40px #ff0044,
0 0 90px rgba(255,0,80,.6);
}
</style>
</head>

<body>

<canvas id="canvas" width="650" height="380"></canvas>

<script>
const c=document.getElementById("canvas");
const x=c.getContext("2d");

let tY=185,dir=1;

const cx=c.width/2;
const cy=c.height/2;

const hearts=[...Array(220)].map(()=>({
x:(Math.random()-0.5)*400,
y:(Math.random()-0.5)*300,
z:Math.random()*800
}));

function bg(){
const g=x.createLinearGradient(0,0,c.width,c.height);
g.addColorStop(0,"#ffd1e4");
g.addColorStop(1,"#ff0033");
x.fillStyle=g;
x.fillRect(0,0,c.width,c.height);
}

function drawHeart(px,py,s){
x.beginPath();
x.moveTo(px,py);
x.bezierCurveTo(px-s,py-s,px-2*s,py+s,px,py+2*s);
x.bezierCurveTo(px+2*s,py+s,px+s,py-s,px,py);
x.fill();
}

function tunnelHearts(){
hearts.forEach(h=>{
h.z-=4;
if(h.z<1)h.z=800;

const scale=300/h.z;
const px=h.x*scale+cx;
const py=h.y*scale+cy;
const size=scale*6;

x.fillStyle="rgba(255,0,80,.8)";
drawHeart(px,py,size);
});
}

function drawText(){
x.textAlign="center";
x.shadowColor="#ff0044";
x.shadowBlur=40;

x.font="700 36px Playfair Display";
x.fillStyle="#b3005e";
x.fillText("Welcome to 2026 🙏",c.width/2,tY);

x.font="300 18px Poppins";
x.fillText("duniya khatam nahi hue?",c.width/2,tY+42);
}

function animate(){
x.clearRect(0,0,c.width,c.height);

bg();
tunnelHearts();
drawText();

tY+=.4*dir;
if(tY>190||tY<175)dir*=-1;

requestAnimationFrame(animate);
}

animate();
</script>

</body>
</html>


