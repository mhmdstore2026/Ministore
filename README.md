<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>MiniStore Pro</title>

<style>
:root {
    --bg: #09090f;
    --panel: #15151f;
    --purple: #8b5cf6;
    --light: #c4b5fd;
    --muted: #aaa9bb;
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    background: var(--bg);
    color: #f5f5f7;
    font-family: Arial, sans-serif;
}

header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 20px 6%;
    background: #101018;
    border-bottom: 1px solid #282838;
}

.logo {
    font-size: 23px;
    font-weight: bold;
    color: #a78bfa;
}

.logo span {
    color: white;
}

button {
    cursor: pointer;
    font-weight: bold;
}

.cart-button {
    background: var(--purple);
    color: white;
    border: none;
    padding: 12px 17px;
    border-radius: 12px;
}

.hero {
    margin: 30px 6%;
    padding: 45px 28px;
    border-radius: 24px;
    border: 1px solid #30243f;
    background:
        radial-gradient(circle at 85% 20%, #5531a7 0%, transparent 35%),
        linear-gradient(135deg, #191326, #101018 70%);
}

.hero small {
    color: #bda8ff;
    letter-spacing: 3px;
}

.hero h1 {
    font-size: 38px;
    margin: 18px 0;
    line-height: 1.2;
}

.hero p {
    color: var(--muted);
    max-width: 420px;
    line-height: 1.6;
}

.hero button {
    margin-top: 25px;
    background: #a78bfa;
    color: #100b1b;
    border: none;
    padding: 14px 22px;
    border-radius: 12px;
}

.section {
    padding: 15px 6% 40px;
}

.section-title {
    font-size: 25px;
    margin-bottom: 22px;
}

.search {
    width: 100%;
    background: var(--panel);
    border: 1px solid #2b2b3a;
    color: white;
    padding: 15px;
    border-radius: 13px;
    margin-bottom: 20px;
    outline: none;
}

.search:focus {
    border-color: var(--purple);
}

.categories {
    display: flex;
    gap: 10px;
    overflow-x: auto;
    margin-bottom: 25px;
}

.category {
    background: #171722;
    color: var(--muted);
    border: 1px solid #292938;
    padding: 10px 17px;
    border-radius: 20px;
    white-space: nowrap;
}

.category.active,
.category:hover {
    background: var(--purple);
    color: white;
}

.products {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 15px;
}

.product {
    background: var(--panel);
    border: 1px solid #292938;
    border-radius: 18px;
    padding: 15px;
    transition: 0.25s;
}

.product:hover {
    transform: translateY(-5px);
    border-color: var(--purple);
    box-shadow: 0 10px 30px #6d28d922;
}

.product-image {
    height: 125px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: linear-gradient(135deg, #242035, #171722);
    border-radius: 14px;
    font-size: 65px;
    margin-bottom: 15px;
}

.product h3 {
    font-size: 16px;
    margin-bottom: 8px;
}

.product p {
    color: #9291a5;
    font-size: 12px;
    margin-bottom: 15px;
}

.product-bottom {
    display: flex;
    justify-content: space-between;
    align-items: center;
    gap: 8px;
}

.price {
    color: var(--light);
    font-size: 19px;
    font-weight: bold;
}

.add {
    background: var(--purple);
    color: white;
    border: none;
    border-radius: 10px;
    padding: 10px 12px;
}

.cart {
    display: none;
    margin: 20px 6% 40px;
    background: var(--panel);
    border: 1px solid #39304e;
    border-radius: 20px;
    padding: 22px;
}

.cart h2 {
    margin-bottom: 15px;
}

.cart-item {
    display: flex;
    justify-content: space-between;
    gap: 10px;
    padding: 12px 0;
    border-bottom: 1px solid #292938;
    color: #c7c6d5;
}

.total {
    margin-top: 20px;
    font-size: 22px;
    color: var(--light);
    font-weight: bold;
}

.checkout {
    width: 100%;
    margin-top: 18px;
    background: #a78bfa;
    color: #100b1b;
    border: none;
    padding: 14px;
    border-radius: 12px;
}

footer {
    text-align: center;
    padding: 30px;
    color: #77768a;
    border-top: 1px solid #22222d;
}

@media (min-width: 700px) {
    .products {
        grid-template-columns: repeat(4, minmax(0, 1fr));
    }

    .hero h1 {
        font-size: 52px;
    }
}
</style>
</head>

<body>

<header>
    <div class="logo">Mini<span>Store</span> ✦</div>
    <button class="cart-button" onclick="toggleCart()">
        🛒 Cart <span id="cart-count">0</span>
    </button>
</header>

<section class="hero">
    <small>THE NEXT LEVEL OF SHOPPING</small>
    <h1>Discover Your<br>Next Favorite.</h1>
    <p>
        Premium tech. Modern design.
        Discover products made for your lifestyle.
    </p>
    <button onclick="scrollToProducts()">Explore Collection →</button>
</section>

<section class="section" id="shop">
    <h2 class="section-title">Featured Products</h2>

    <input
        class="search"
        id="search"
        placeholder="🔎 Search products..."
        oninput="renderProducts()"
    >

    <div class="categories">
        <button class="category active" onclick="setCategory('All', this)">All</button>
        <button class="category" onclick="setCategory('Audio', this)">Audio</button>
        <button class="category" onclick="setCategory('Wearables', this)">Wearables</button>
        <button class="category" onclick="setCategory('Gaming', this)">Gaming</button>
        <button class="category" onclick="setCategory('Accessories', this)">Accessories</button>
    </div>

    <div class="products" id="products"></div>
</section>

<section class="cart" id="cart">
    <h2>Your Shopping Cart</h2>
    <div id="cart-items"></div>
    <div class="total" id="total">Total: $0</div>
    <button class="checkout" onclick="checkout()">Continue to Checkout</button>
</section>

<footer>
    MiniStore Pro © 2026 · Premium Shopping Experience
</footer>

<script>
const products = [
    {
        name: "Headphones",
        price: 15,
        icon: "🎧",
        category: "Audio",
        description: "Immersive sound experience"
    },
    {
        name: "Smart Watch",
        price: 25,
        icon: "⌚",
        category: "Wearables",
        description: "Style meets technology"
    },
    {
        name: "Gaming Mouse",
        price: 10,
        icon: "🖱️",
        category: "Gaming",
        description: "Precision for every move"
    },
    {
        name: "Keyboard",
        price: 20,
        icon: "⌨️",
        category: "Accessories",
        description: "Designed for your setup"
    }
];

let cart = [];
let selectedCategory = "All";

function renderProducts() {
    const search = document.getElementById("search").value.toLowerCase();

    const filtered = products.filter(product => {
        const matchesCategory =
            selectedCategory === "All" ||
            product.category === selectedCategory;

        const matchesSearch =
            product.name.toLowerCase().includes(search);

        return matchesCategory && matchesSearch;
    });

    document.getElementById("products").innerHTML =
        filtered.map(product => `
            <div class="product">
                <div class="product-image">${product.icon}</div>
                <h3>${product.name}</h3>
                <p>${product.description}</p>
                <div class="product-bottom">
                    <span class="price">$${product.price}</span>
                    <button class="add"
                        onclick="addToCart('${product.name}')">
                        + Add
                    </button>
                </div>
            </div>
        `).join("");
}

function setCategory(category, button) {
    selectedCategory = category;

    document.querySelectorAll(".category").forEach(item => {
        item.classList.remove("active");
    });

    button.classList.add("active");
    renderProducts();
}

function addToCart(name) {
    const product = products.find(item => item.name === name);
    cart.push(product);
    updateCart();
}

function updateCart() {
    document.getElementById("cart-count").textContent = cart.length;

    document.getElementById("cart-items").innerHTML =
        cart.map((item, index) => `
            <div class="cart-item">
                <span>${item.icon} ${item.name} — $${item.price}</span>
                <button class="add" onclick="removeItem(${index})">×</button>
            </div>
        `).join("");

    const total = cart.reduce((sum, item) => sum + item.price, 0);

    document.getElementById("total").textContent = "Total: $" + total;
}

function removeItem(index) {
    cart.splice(index, 1);
    updateCart();
}

function toggleCart() {
    const cartBox = document.getElementById("cart");

    cartBox.style.display =
        cartBox.style.display === "block" ? "none" : "block";

    cartBox.scrollIntoView({ behavior: "smooth" });
}

function scrollToProducts() {
    document.getElementById("shop").scrollIntoView({
        behavior: "smooth"
    });
}

function checkout() {
    if (cart.length === 0) {
        alert("Your cart is empty!");
        return;
    }

    const total = cart.reduce((sum, item) => sum + item.price, 0);

    alert("Demo checkout successful! Total: $" + total);

    cart = [];
    updateCart();
    document.getElementById("cart").style.display = "none";
}

renderProducts();
</script>

</body>
  </html>
