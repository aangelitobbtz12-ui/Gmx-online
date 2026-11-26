
<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>GMX ONLINE</title>
<style>
*{box-sizing:border-box}
body{margin:0;background:#101010;color:white;font-family:Arial}
header{text-align:center;background:#1b1b1b;padding:20px;border-bottom:3px solid #e00032}
header h1{font-size:40px;color:#ff1744;margin:0}
header p{letter-spacing:5px;margin:4px}
.hero{text-align:center;padding:28px 12px;background:linear-gradient(130deg,#550015,#111)}
.hero h2{font-size:25px}
main{max-width:850px;margin:auto;padding:15px}
.notice{background:#480d19;border:1px solid #ff3153;padding:15px;border-radius:10px;text-align:center;color:white;font-weight:bold}
h2.section{border-left:4px solid #ff1744;padding-left:10px;margin-top:28px}
.products{display:grid;grid-template-columns:repeat(2,1fr);gap:12px}
.product{background:#202020;padding:15px;border-radius:12px;text-align:center;border:1px solid #383838}
.icon{font-size:30px}
.price{color:#ff526d;font-size:20px;font-weight:bold}
button{background:#e90032;color:white;border:0;border-radius:8px;padding:12px;font-weight:bold;cursor:pointer}
.product button{width:100%}
.cart{background:#202020;padding:17px;border-radius:12px;margin-top:25px}
input,select{width:100%;padding:13px;margin:8px 0;background:#303030;color:white;border:1px solid #555;border-radius:7px}
.item{padding:9px 0;border-bottom:1px solid #444}
footer{text-align:center;padding:25px;color:#aaa}
@media(max-width:400px){.products{grid-template-columns:1fr}}
</style>
</head>
<body>
<header>
<h1>GMX</h1>
<p>ONLINE</p>
</header>

<section class="hero">
<h2>BIENVENIDO A GMX ONLINE</h2>
<p>💎 DIAMANTES | 🎁 CAJITAS | 🔹 FRAGMENTOS</p>
</section>

<main>
<div class="notice">
⚠️ PREGUNTAR POR STOCK DISPONIBLE
ANTES DE REALIZAR UNA COMPRA
</div>

<div id="catalog"></div>

<section class="cart">
<h2>🛒 MI CARRITO</h2>
<div id="cart">Tu carrito está vacío.</div>
<h2 id="total">TOTAL: $0 MXN</h2>

<h3>Datos del pedido</h3>
<input id="player" placeholder="ID de jugador Free Fire">
<select id="payment">
<option value="">Selecciona método de pago</option>
<option>Mercado Pago</option>
<option>Transferencia bancaria</option>
</select>
<button onclick="checkout()">REALIZAR PEDIDO</button>
<p id="message"></p>
</section>

<footer>
GMX ONLINE © 2026
<br>
Tu tienda de Free Fire
</footer>

<script>
const categories=[
{
title:"💎 DIAMANTES — MÉXICO",
items:[
["110 Diamantes",19],
["341 Diamantes",58],
["572 Diamantes",85],
["1166 Diamantes",175],
["2396 Diamantes",315],
["6160 Diamantes",730]
]
},
{
title:"🔹 FRAGMENTOS UNIVERSALES",
items:[
["900 Fragmentos",850],
["800 Fragmentos",710],
["700 Fragmentos",605],
["600 Fragmentos",500],
["500 Fragmentos",470],
["400 Fragmentos",359],
["300 Fragmentos",292],
["200 Fragmentos",198]
]
},
{
title:"🎁 CAJITAS EVOLUTIVAS",
items:[
["50 Cajitas",200],
["100 Cajitas",385],
["150 Cajitas",550],
["200 Cajitas",685],
["250 Cajitas",800],
["300 Cajitas",975]
]
}
];

let cart=[];

function renderCatalog(){
document.getElementById("catalog").innerHTML=
categories.map((cat,c)=>`
<h2 class="section">${cat.title}</h2>
<div class="products">
${cat.items.map((p,i)=>`
<div class="product">
<div class="icon">${c===0?"💎":c===1?"🔹":"🎁"}</div>
<h3>${p[0]}</h3>
<div class="price">$${p[1]} MXN</div>
<button onclick="add(${c},${i})">AGREGAR</button>
</div>`).join("")}
</div>`).join("");
}

function add(c,i){
let p=categories[c].items[i];
cart.push({name:p[0],price:p[1]});
renderCart();
}

function removeItem(i){
cart.splice(i,1);
renderCart();
}


function renderCart(){
 let total=cart.reduce((s,p)=>s+p.price,0);

 document.getElementById("cart").innerHTML=cart.length?
 cart.map((p,i)=>`
 <div class="item">
 ${p.name} - $${p.price} MXN
 <button onclick="removeItem(${i})">Quitar</button>
 </div>
 `).join(""):"Tu carrito está vacío.";

 document.getElementById("total").textContent=
 "TOTAL: $"+total+" MXN";
}
 

function checkout(){
 const id=document.getElementById("player").value.trim();
 const payment=document.getElementById("payment").value;

 if(!cart.length)return alert("Agrega productos");
 if(!id)return alert("Escribe tu ID");
 if(!payment)return alert("Selecciona un pago");

 const total=cart.reduce((s,p)=>s+p.price,0);

 const products=cart.map(p=>
 "• "+p.name+" - $"+p.price+" MXN"
 ).join("\n");

 const message=
 "🔥 GMX ONLINE - NUEVO PEDIDO\n"+
 "ID: "+id+"\n\n"+
 products+"\n\n"+
 "TOTAL: $"+total+" MXN\n"+
 "Pago: "+payment+"\n"+
 "Favor de confirmar stock.";

 const url="https://wa.me/527226449648?text="+
 encodeURIComponent(message);

 window.location.href=url;
}
 
renderCatalog();
renderCart();
</script>
</body>
</html>
