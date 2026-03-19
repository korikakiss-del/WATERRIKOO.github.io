<!DOCTYPE html>
<html lang="hu">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">

<title>Rikoo GOD TIER</title>

<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@300;500;700&display=swap" rel="stylesheet">

<style>
body {
    margin:0;
    font-family:'Poppins',sans-serif;
    background:#020617;
    color:white;
    overflow-x:hidden;
}

/* PARTICLE BACKGROUND */
canvas {
    position:fixed;
    top:0;
    left:0;
    z-index:-1;
}

/* HEADER */
header {
    display:flex;
    justify-content:space-between;
    padding:20px;
    background:#000;
}

.logo {
    color:#00eaff;
    font-size:24px;
    font-weight:700;
}

.search input {
    padding:10px;
    border-radius:10px;
    border:none;
}

/* HERO */
.hero {
    text-align:center;
    padding:60px;
}

.hero h1 {
    font-size:50px;
    background:linear-gradient(90deg,#00eaff,#007cf0);
    -webkit-background-clip:text;
    color:transparent;
}

/* GRID */
.products {
    display:grid;
    grid-template-columns:repeat(auto-fill,minmax(180px,1fr));
    gap:20px;
    padding:20px;
}

.card {
    background:#111827;
    padding:15px;
    border-radius:12px;
    text-align:center;
    transition:0.3s;
}

.card:hover {
    transform:translateY(-10px) scale(1.05);
    box-shadow:0 0 20px #00eaff;
}

.price {color:#00eaff;}

button {
    background:#00eaff;
    border:none;
    padding:6px;
    border-radius:6px;
    cursor:pointer;
}

/* CART */
.cartIcon {
    position:fixed;
    bottom:20px;
    right:20px;
    background:#00eaff;
    color:black;
    padding:15px;
    border-radius:50px;
    cursor:pointer;
}

.cartPanel {
    position:fixed;
    right:-350px;
    top:0;
    width:320px;
    height:100%;
    background:#111827;
    padding:20px;
    transition:0.3s;
    overflow-y:auto;
}

.cartPanel.open {right:0;}

.cartItem {
    display:flex;
    justify-content:space-between;
    margin:10px 0;
}

/* LEVEL SYSTEM */
.levelBox {
    position:fixed;
    top:80px;
    right:20px;
    background:#111827;
    padding:10px;
    border-radius:10px;
}

/* STATS */
.stats {
    display:flex;
    justify-content:space-around;
    padding:40px;
}

.stat h2 {
    color:#00eaff;
}

/* FOOTER */
footer {
    text-align:center;
    padding:20px;
    opacity:0.5;
}
</style>
</head>

<body>

<canvas id="bg"></canvas>

<header>
<div class="logo">💧 Rikoo GOD</div>
<div class="search">
<input type="text" id="search" placeholder="Keresés..." onkeyup="searchProduct()">
</div>
</header>

<div class="hero">
<h1>MAX ENERGY MODE ⚡</h1>
<p>Ez már nem víz. Ez egy rendszer.</p>
</div>

<div class="products" id="products"></div>

<div class="stats">
<div class="stat"><h2>5M+</h2><p>Felhasználó</p></div>
<div class="stat"><h2>999</h2><p>Szint</p></div>
<div class="stat"><h2>∞</h2><p>Energia</p></div>
</div>

<!-- LEVEL -->
<div class="levelBox">
Szint: <span id="level">1</span><br>
XP: <span id="xp">0</span>
</div>

<!-- CART -->
<div class="cartIcon" onclick="toggleCart()">🛒 <span id="count">0</span></div>

<div class="cartPanel" id="cartPanel">
<h2>Kosár</h2>
<button style="float:right; background:#ff4d4d; border:none; border-radius:6px; padding:5px 10px; cursor:pointer;" onclick="toggleCart()">❌ Bezárás</button>
<div id="cartItems"></div>
<p>Összesen: <span id="total">0</span> Ft</p>
</div>

<footer>Rikoo ENERGY GOD SYSTEM</footer>

<script>
let products = [
  "Aqua Blast", "Neon Wave", "Storm Surge", "Crystal Drop", "Lightning Bolt",
  "Frozen Stream", "Solar Splash", "Hyper Tide", "Glacial Rush", "Blue Inferno",
  "Turbo Current", "Electro Flow", "Plasma Mist", "Quantum Liquid", "Aurora Stream",
  "Cosmic Drop", "Vortex Splash", "Hydro Charge", "Liquid Nova", "Photon Wave",
  "Zen Waterfall", "Ice Surge", "Thunder Stream", "Galaxy Flow", "Turbo Aqua",
  "Liquid Lightning", "Neon Frost", "Abyssal Tide", "Crystal Surge", "Liquid Blaze",
  "Vapor Rush", "Shockwave Drop", "Tsunami Twist", "Blizzard Flow", "Starlight Splash",
  "Electric Drift", "Hydro Burst", "Frostfire Stream", "Aurora Mist", "Quantum Splash",
  "Liquid Pulse", "Photon Surge", "Cosmic Wave", "Turbo Frost", "Neon Stream",
  "Ice Blaze", "Hyper Current", "Liquid Thunder", "Storm Drift", "Glacial Wave"
];

let cart=JSON.parse(localStorage.getItem("cart"))||[];
let xp=0;
let level=1;

/* RENDER */
function renderProducts(list=products){
let html="";
list.forEach(p=>{
html+=`
<div class="card">
<h3>${p}</h3>
<div class="price">1999 Ft</div>
<button onclick="addToCart('${p}')">Kosárba</button>
</div>`;});
document.getElementById("products").innerHTML=html;
}

/* CART */
function addToCart(p){
cart.push(p);
xp+=10;
checkLevel();
save();
renderCart();
}

function removeItem(i){
cart.splice(i,1);
save();
renderCart();
}

function renderCart(){
let html="";
let total=0;

cart.forEach((item,i)=>{
total+=1999;
html+=`
<div class="cartItem">
${item}
<span onclick="removeItem(${i})">❌</span>
</div>`;});

document.getElementById("cartItems").innerHTML=html;
document.getElementById("count").innerText=cart.length;
document.getElementById("total").innerText=total;
}

/* LEVEL */
function checkLevel(){
if(xp>=100){
level++;
xp=0;
alert("Szintlépés! 😎");
}
document.getElementById("xp").innerText=xp;
document.getElementById("level").innerText=level;
}

/* SEARCH */
function searchProduct(){
let val=document.getElementById("search").value.toLowerCase();
let filtered=products.filter(p=>p.toLowerCase().includes(val));
renderProducts(filtered);
}

/* SAVE */
function save(){
localStorage.setItem("cart",JSON.stringify(cart));
}

/* CART TOGGLE */
function toggleCart(){
document.getElementById("cartPanel").classList.toggle("open");
}

/* PARTICLE BACKGROUND */
let canvas=document.getElementById("bg");
let ctx=canvas.getContext("2d");
canvas.width=window.innerWidth;
canvas.height=window.innerHeight;

let particles=[];

for(let i=0;i<100;i++){
particles.push({x:Math.random()*canvas.width,y:Math.random()*canvas.height,v:Math.random()});
}

function animate(){
ctx.clearRect(0,0,canvas.width,canvas.height);
particles.forEach(p=>{
p.y+=p.v;
if(p.y>canvas.height)p.y=0;
ctx.fillStyle="#00eaff";
ctx.fillRect(p.x,p.y,2,2);
});
requestAnimationFrame(animate);
}
animate();

renderProducts();
renderCart();
</script>

</body>
</html>
