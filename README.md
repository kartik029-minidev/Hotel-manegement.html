<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Hotel Service - Kartik</title>
  <style>
    body {
      font-family: "Segoe UI", Tahoma, sans-serif;
      background: linear-gradient(to right, #f9f9f9, #ececec);
      margin: 0;
      padding: 0;
      color: #333;
    }

    header {
      background: #2c3e50;
      color: #fff;
      padding: 20px;
      text-align: center;
      font-size: 22px;
      box-shadow: 0 4px 6px rgba(0,0,0,0.2);
    }

    nav {
      display: flex;
      justify-content: center;
      background: #34495e;
      padding: 10px 0;
    }

    nav button {
      background: #1abc9c;
      border: none;
      color: white;
      padding: 12px 20px;
      margin: 0 10px;
      cursor: pointer;
      font-size: 16px;
      border-radius: 8px;
      transition: background 0.3s;
    }

    nav button:hover {
      background: #16a085;
    }

    .section {
      display: none;
      padding: 20px;
      animation: fadeIn 0.5s ease-in-out;
    }

    .active {
      display: block;
    }

    @keyframes fadeIn {
      from {opacity: 0;}
      to {opacity: 1;}
    }

    .card {
      background: #fff;
      border-radius: 12px;
      padding: 25px;
      box-shadow: 0 6px 12px rgba(0,0,0,0.1);
      max-width: 600px;
      margin: 20px auto;
    }

    .card h2 {
      margin-top: 0;
      color: #2c3e50;
    }

    label {
      font-weight: bold;
      display: block;
      margin: 10px 0 5px;
    }

    select, input[type="number"], button {
      padding: 10px;
      border-radius: 8px;
      border: 1px solid #ccc;
      width: 100%;
      font-size: 15px;
      margin: 8px 0;
    }

    input[type="number"] {
      width: 80px;
      text-align: center;
    }

    .dish-option {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin: 8px 0;
      padding: 8px;
      background: #f9f9f9;
      border-radius: 6px;
    }

    button {
      background: #1abc9c;
      color: white;
      font-weight: bold;
      cursor: pointer;
      border: none;
      transition: background 0.3s;
    }

    button:hover {
      background: #16a085;
    }

    ul {
      list-style: none;
      padding: 0;
    }

    .order-item {
      background: #f4f4f4;
      padding: 10px;
      border-radius: 6px;
      margin: 8px 0;
      display: flex;
      align-items: center;
    }

    .order-item input[type="checkbox"] {
      margin-right: 10px;
    }

    footer {
      text-align: center;
      background: #2c3e50;
      color: white;
      padding: 15px;
      margin-top: 20px;
      font-size: 14px;
    }

    a {
      color: #1abc9c;
      text-decoration: none;
    }

    a:hover {
      text-decoration: underline;
    }
  </style>
</head>
<body>
  <header>
    🍴 Welcome to Vim City Hotel Service
  </header>

  <nav>
    <button onclick="showSection('placeOrder')">Place Order</button>
    <button onclick="checkPassword()">See Order</button>
    <button onclick="showSection('developer')">About Developer</button>
  </nav>

  <!-- Place Order Section -->
  <div id="placeOrder" class="section">
    <div class="card">
      <h2>Place an Order</h2>
      <label>Select Table:</label>
      <select id="tableSelect">
        <option value="">-- Choose a Table --</option>
        <option value="Table 1">Table 1</option>
        <option value="Table 2">Table 2</option>
        <option value="Table 3">Table 3</option>
        <option value="Table 4">Table 4</option>
      </select>

      <label>Select Dishes & Quantity:</label>
      <div class="dish-option">
        <span>Pizza</span>
        <input type="number" min="0" max="10" value="0" id="dish-Pizza">
      </div>
      <div class="dish-option">
        <span>Burger</span>
        <input type="number" min="0" max="10" value="0" id="dish-Burger">
      </div>
      <div class="dish-option">
        <span>Pasta</span>
        <input type="number" min="0" max="10" value="0" id="dish-Pasta">
      </div>
      <div class="dish-option">
        <span>Noodles</span>
        <input type="number" min="0" max="10" value="0" id="dish-Noodles">
      </div>
      <div class="dish-option">
        <span>Sandwich</span>
        <input type="number" min="0" max="10" value="0" id="dish-Sandwich">
      </div>

      <button onclick="placeOrder()">✅ Place Order</button>
    </div>
  </div>

  <!-- See Order Section -->
  <div id="seeOrder" class="section">
    <div class="card">
      <h2>Current Orders</h2>
      <ul id="orderList"></ul>
    </div>
  </div>

  <!-- About Developer -->
  <div id="developer" class="section">
    <div class="card">
      <h2>About Developer</h2>
      <p>This website is developed by <b>Kartik Saxena</b>, lives in Vim City.</p>
      <p>To place order of more such websites mail: 
        <a href="mailto:kartiksaxena029@gmail.com">kartiksaxena029@gmail.com</a>
      </p>
      <p>Follow me on GitHub: 
        <a href="https://github.com/kartik029-minidev" target="_blank">kartik029-minidev</a>
      </p>
    </div>
  </div>

  <footer>
    © 2025 Vim City Hotel Service | Designed with ❤️
  </footer>

  <script>
    let orders = [];

    function showSection(id) {
      document.querySelectorAll('.section').forEach(sec => sec.classList.remove('active'));
      document.getElementById(id).classList.add('active');
    }

    function checkPassword() {
      let pass = prompt("Enter password to view orders:");
      if (pass === "kartik029-minidev") {
        showSection('seeOrder');
        loadOrders();
      } else {
        alert("Incorrect password!");
      }
    }

    function placeOrder() {
      let table = document.getElementById('tableSelect').value;
      if (!table) {
        alert("Please select a table first!");
        return;
      }

      let dishes = [];
      let dishNames = ["Pizza", "Burger", "Pasta", "Noodles", "Sandwich"];

      dishNames.forEach(dish => {
        let qty = parseInt(document.getElementById("dish-" + dish).value);
        if (qty > 0) {
          dishes.push(`${dish} (${qty})`);
        }
      });

      if (dishes.length === 0) {
        alert("Please select at least one dish with quantity!");
        return;
      }

      let order = { table: table, dishes: dishes };
      orders.push(order);

      alert("Order placed successfully!");
      document.getElementById('tableSelect').value = "";
      dishNames.forEach(dish => {
        document.getElementById("dish-" + dish).value = 0;
      });
    }

    function loadOrders() {
      let list = document.getElementById('orderList');
      list.innerHTML = "";
      orders.forEach((order, index) => {
        let li = document.createElement('li');
        li.className = "order-item";
        li.innerHTML = `<input type="checkbox" onchange="removeOrder(${index})"> 
                        <b>${order.table}</b>: ${order.dishes.join(", ")}`;
        list.appendChild(li);
      });
    }

    function removeOrder(index) {
      orders.splice(index, 1);
      loadOrders();
    }
  </script>
</body>
</html>
