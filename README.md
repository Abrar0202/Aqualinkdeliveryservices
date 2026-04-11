<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>FreshMart Grocery - Advanced</title>
  <style>
    *{margin:0;padding:0;box-sizing:border-box;font-family:Arial, sans-serif;}
    body{background:#f4f6f8;}

    header{
      background:linear-gradient(135deg,#16a34a,#15803d);
      color:white;
      padding:20px;
      text-align:center;
    }

    nav{
      background:#111;
      display:flex;
      justify-content:center;
      flex-wrap:wrap;
      gap:15px;
      padding:10px;
    }

    nav a{
      color:white;
      text-decoration:none;
      font-weight:bold;
    }

    .container{padding:20px;}

    .top-bar{
      display:flex;
      gap:10px;
      flex-wrap:wrap;
      margin-bottom:20px;
    }

    input, select{
      padding:10px;
      border:1px solid #ccc;
      border-radius:8px;
      flex:1;
    }

    .grid{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(220px,1fr));
      gap:15px;
    }

    .card{
      background:white;
      border-radius:12px;
      overflow:hidden;
      box-shadow:0 4px 10px rgba(0,0,0,0.1);
      transition:0.3s;
    }

    .card:hover{transform:scale(1.03);}

    .card img{
      width:100%;
      height:160px;
      object-fit:cover;
    }

    .card-body{padding:10px;}

    .price{color:green;font-weight:bold;}

    button{
      background:#16a34a;
      color:white;
      border:none;
      padding:10px;
      width:100%;
      cursor:pointer;
      border-radius:8px;
      margin-top:8px;
    }

    button:hover{background:#15803d;}

    .cart{
      background:white;
      padding:15px;
      border-radius:10px;
      margin-top:20px;
    }

    .cart-item{
      display:flex;
      justify-content:space-between;
      align-items:center;
      padding:8px 0;
      border-bottom:1px solid #eee;
    }

    .remove-btn{
      background:red;
      padding:5px 10px;
      border:none;
      color:white;
      border-radius:6px;
      cursor:pointer;
      width:auto;
    }

    .remove-btn:hover{background:darkred;}

    footer{
      text-align:center;
      padding:20px;
      background:#111;
      color:white;
      margin-top:30px;
    }

    .badge{
      background:red;
      color:white;
      padding:2px 8px;
      border-radius:50%;
      font-size:12px;
      margin-left:5px;
    }
  </style>
</head>
<body>

<header>
  <h1>FreshMart Grocery</h1>
  <p>Advanced Grocery Store System</p>
</header>

<nav>
  <a href="#">Home</a>
  <a href="#shop">Shop</a>
  <a href="#cartSection">Cart <span id="cartCount" class="badge">0</span></a>
</nav>

<div class="container">

  <div class="top-bar">
    <input type="text" id="search" placeholder="Search products..." onkeyup="renderProducts()" />
    <select id="category" onchange="renderProducts()">
      <option value="all">All Categories</option>
      <option value="fruits">Fruits</option>
      <option value="dairy">Dairy</option>
      <option value="bakery">Bakery</option>
    </select>
  </div>

  <div id="shop" class="grid"></div>

  <div id="cartSection" class="cart">
    <h2>Your Cart</h2>
    <div id="cartItems"></div>
    <h3 id="total">Total: $0</h3>
    <button onclick="checkout()">Checkout</button>
  </div>

</div>

<footer>
  © 2026 FreshMart Grocery | Advanced Version
</footer>

<script>

const products = [
  {id:1,name:"Apple",price:2,cat:"fruits",img:"https://source.unsplash.com/300x200/?apple"},
  {id:2,name:"Banana",price:1,cat:"fruits",img:"https://source.unsplash.com/300x200/?banana"},
  {id:3,name:"Milk",price:1.5,cat:"dairy",img:"https://source.unsplash.com/300x200/?milk"},
  {id:4,name:"Cheese",price:3,cat:"dairy",img:"https://source.unsplash.com/300x200/?cheese"},
  {id:5,name:"Bread",price:2,cat:"bakery",img:"https://source.unsplash.com/300x200/?bread"}
];

let cart = JSON.parse(localStorage.getItem("cart")) || [];

function renderProducts(){
  let search = document.getElementById("search").value.toLowerCase();
  let category = document.getElementById("category").value;

  let filtered = products.filter(p=>{
    return (category === "all" || p.cat === category) && p.name.toLowerCase().includes(search);
  });

  let html = "";
  filtered.forEach(p=>{
    html += `
      <div class='card'>
        <img src='${p.img}' />
        <div class='card-body'>
          <h3>${p.name}</h3>
          <p class='price'>$${p.price}</p>
          <button onclick='addToCart(${p.id})'>Add to Cart</button>
        </div>
      </div>
    `;
  });

  document.getElementById("shop").innerHTML = html;
}

function addToCart(id){
  let item = products.find(p=>p.id===id);
  cart.push(item);
  localStorage.setItem("cart",JSON.stringify(cart));
  updateCart();
}

function updateCart(){
  let html="";
  let total=0;

  cart.forEach((c,i)=>{
    total += c.price;
    html += `<div class='cart-item'>${c.name} - $${c.price} <button class='remove-btn' onclick='removeItem(${i})'>Remove</button></div>`;
  });

  document.getElementById("cartItems").innerHTML = html;
  document.getElementById("total").innerText = "Total: $" + total;
  document.getElementById("cartCount").innerText = cart.length;
}

function removeItem(index){
  if(confirm("Are you sure you want to remove this item?")){
    cart.splice(index,1);
    localStorage.setItem("cart",JSON.stringify(cart));
    updateCart();
  }
}

function checkout(){
  alert("Order placed successfully!");
  cart = [];
  localStorage.setItem("cart",JSON.stringify(cart));
  updateCart();
}

renderProducts();
updateCart();

</script>

</body>
</html>
