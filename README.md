<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>FreshMart Grocery Store</title>
  <style>
    *{margin:0;padding:0;box-sizing:border-box;font-family:Arial,sans-serif;}
    body{background:#f4f6f8;}

    header{
      background:linear-gradient(135deg,#16a34a,#15803d);
      color:white;
      text-align:center;
      padding:20px;
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

    input{
      padding:10px;
      border:1px solid #ccc;
      border-radius:8px;
      flex:1;
    }

    button{
      padding:10px 15px;
      border:none;
      background:#111;
      color:white;
      border-radius:8px;
      cursor:pointer;
    }

    button:hover{background:#333;}

    .grid{
      display:grid;
      grid-template-columns:repeat(auto-fit,minmax(200px,1fr));
      gap:15px;
    }

    .card{
      background:white;
      border-radius:10px;
      overflow:hidden;
      box-shadow:0 4px 10px rgba(0,0,0,0.1);
    }

    .card img{
      width:100%;
      height:160px;
      object-fit:cover;
    }

    .card-body{padding:10px;}

    .price{color:green;font-weight:bold;}

    .cart{
      background:white;
      padding:15px;
      margin-top:20px;
      border-radius:10px;
    }

    .cart-item{
      display:flex;
      justify-content:space-between;
      padding:5px 0;
    }

    .remove{
      background:red;
      padding:5px 10px;
      border:none;
      color:white;
      border-radius:6px;
      cursor:pointer;
    }

    .contact{
      background:white;
      padding:15px;
      margin-top:20px;
      border-radius:10px;
    }

    .whatsapp{
      position:fixed;
      bottom:20px;
      right:20px;
      background:#25D366;
      color:white;
      padding:15px;
      border-radius:50px;
      text-decoration:none;
      font-weight:bold;
    }

    .checkout-box{
      background:white;
      padding:15px;
      margin-top:20px;
      border-radius:10px;
    }
  </style>
</head>
<body>

<header>
  <h1>FreshMart Grocery Store</h1>
  <p>All Daily Essentials in One Place</p>
</header>

<nav>
  <a href="#shop">Shop</a>
  <a href="#cart">Cart</a>
  <a href="#contact">Contact</a>
</nav>

<div class="container">

  <div class="top-bar">
    <input type="text" id="search" placeholder="Search products..." onkeyup="renderProducts()" />
    <button onclick="renderProducts()">Search</button>
  </div>

  <div id="shop" class="grid"></div>

  <div id="cart" class="cart">
    <h2>Your Cart</h2>
    <div id="cartItems"></div>
    <h3 id="total">Total: $0</h3>
    <button onclick="checkout()">Checkout</button>
  </div>

  <div id="checkoutBox" class="checkout-box" style="display:none">
    <h2>Order Placed Successfully ✅</h2>
    <p id="orderSummary"></p>
  </div>

  <div id="contact" class="contact">
    <h2>Contact Details</h2>
    <p><b>Mobile NO:</b> <a href="tel:+97400000000">+974 00000000</a></p>
    <p><b>Email ID:</b> <a href="mailto:freshmart@gmail.com">freshmart@gmail.com</a></p>
    <p><b>Website:</b> <a href="https://www.freshmart.com" target="_blank">www.freshmart.com</a></p>
  </div>

</div>

<a class="whatsapp" href="https://wa.me/97400000000" target="_blank">WhatsApp Chat</a>

<script>

const products = [
  {name:"Apple",price:2,img:"https://source.unsplash.com/400x300/?apple"},
  {name:"Banana",price:1,img:"https://source.unsplash.com/400x300/?banana"},
  {name:"Carrots",price:2,img:"https://source.unsplash.com/400x300/?carrot"},
  {name:"Tomatoes",price:2,img:"https://source.unsplash.com/400x300/?tomato"},
  {name:"Lettuce",price:2,img:"https://source.unsplash.com/400x300/?lettuce"},
  {name:"Potatoes",price:3,img:"https://source.unsplash.com/400x300/?potato"},

  {name:"Milk",price:1.5,img:"https://source.unsplash.com/400x300/?milk"},
  {name:"Cheese",price:3,img:"https://source.unsplash.com/400x300/?cheese"},
  {name:"Yogurt",price:2,img:"https://source.unsplash.com/400x300/?yogurt"},
  {name:"Butter",price:2.5,img:"https://source.unsplash.com/400x300/?butter"},
  {name:"Eggs",price:2,img:"https://source.unsplash.com/400x300/?eggs"},

  {name:"Pasta",price:2,img:"https://source.unsplash.com/400x300/?pasta"},
  {name:"Rice",price:5,img:"https://source.unsplash.com/400x300/?rice"},
  {name:"Spices",price:3,img:"https://source.unsplash.com/400x300/?spices"},
  {name:"Herbs",price:2,img:"https://source.unsplash.com/400x300/?herbs"},
  {name:"Sauces",price:3,img:"https://source.unsplash.com/400x300/?sauce"},
  {name:"Oil",price:6,img:"https://source.unsplash.com/400x300/?oil"},
  {name:"Vinegar",price:2,img:"https://source.unsplash.com/400x300/?vinegar"},

  {name:"Bread",price:2,img:"https://source.unsplash.com/400x300/?bread"},
  {name:"Buns",price:2,img:"https://source.unsplash.com/400x300/?buns"},
  {name:"Bagels",price:3,img:"https://source.unsplash.com/400x300/?bagels"},
  {name:"Tortillas",price:3,img:"https://source.unsplash.com/400x300/?tortilla"},

  {name:"Chicken",price:6,img:"https://source.unsplash.com/400x300/?chicken"},
  {name:"Beef",price:8,img:"https://source.unsplash.com/400x300/?beef"},
  {name:"Fish",price:7,img:"https://source.unsplash.com/400x300/?fish"},
  {name:"Pork",price:7,img:"https://source.unsplash.com/400x300/?pork"},

  {name:"Ice Cream",price:4,img:"https://source.unsplash.com/400x300/?icecream"},
  {name:"Frozen Vegetables",price:3,img:"https://source.unsplash.com/400x300/?frozen-vegetables"},
  {name:"Ready Meals",price:5,img:"https://source.unsplash.com/400x300/?ready-meal"},

  {name:"Coffee",price:4,img:"https://source.unsplash.com/400x300/?coffee"},
  {name:"Tea",price:3,img:"https://source.unsplash.com/400x300/?tea"},
  {name:"Juice",price:3,img:"https://source.unsplash.com/400x300/?juice"},
  {name:"Soda",price:2,img:"https://source.unsplash.com/400x300/?soda"},

  {name:"Cleaning Supplies",price:5,img:"https://source.unsplash.com/400x300/?cleaning"},
  {name:"Toilet Paper",price:3,img:"https://source.unsplash.com/400x300/?toilet-paper"},
  {name:"Soap",price:2,img:"https://source.unsplash.com/400x300/?soap"}
];

let cart=[];

function renderProducts(){
  let search=document.getElementById("search").value.toLowerCase();
  let html="";

  products.filter(p=>p.name.toLowerCase().includes(search)).forEach(p=>{
    html+=`
      <div class='card'>
        <img src='${p.img}' />
        <div class='card-body'>
          <h3>${p.name}</h3>
          <p class='price'>$${p.price}</p>
          <button onclick='addToCart("${p.name}",${p.price})'>Add</button>
        </div>
      </div>
    `;
  });

  document.getElementById("shop").innerHTML=html;
}

function addToCart(name,price){
  cart.push({name,price});
  updateCart();
}

function removeItem(i){
  cart.splice(i,1);
  updateCart();
}

function updateCart(){
  let html="";
  let total=0;

  cart.forEach((c,i)=>{
    total+=c.price;
    html+=`
      <div class='cart-item'>
        ${c.name} - $${c.price}
        <button class='remove' onclick='removeItem(${i})'>X</button>
      </div>
    `;
  });

  document.getElementById("cartItems").innerHTML=html;
  document.getElementById("total").innerText="Total: $"+total;
}

function checkout(){
  if(cart.length===0){ alert("Cart is empty!"); return; }

  let summary = cart.map(c=>c.name+" ($"+c.price+")").join(", ");

  document.getElementById("orderSummary").innerText = summary;
  document.getElementById("checkoutBox").style.display = "block";

  cart = [];
  updateCart();
}

renderProducts();

</script>

</body>
</html>
