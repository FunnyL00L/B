<template>
  <div id="app">
    <header class="header">
      <img
        src="@/assets/gaming-logo.png"
        alt="Logo Gaming"
        style="max-width: 100px"
      />
      <h1 class="site-name">FiniX13</h1>
    </header>
    <nav>
      <ul>
        <li><a href="#">Produk</a></li>
        <li><a href="#">Servis & Rakit PC</a></li>
        <li><a href="#">Info Garansi</a></li>
        <li><a href="second">Jual Second</a></li>
      </ul>
      <div class="cart" @click="toggleCart">
        <div class="cart-icon">🛒</div>
        <div class="cart-total">Keranjang ({{ cartItems.length }})</div>
      </div>
    </nav>
    <div class="container">
      <div
        class="product"
        v-for="product in formattedProducts"
        :key="product.id"
      >
        <h2>{{ product.title }}</h2>
        <img
          :src="product.image"
          :alt="product.title"
          style="max-width: 100px"
        />
        <p>{{ product.description }}</p>
        <p>
          <strong>{{ product.price }}</strong>
        </p>
        <button @click="addToCart(product)">Tambah ke Keranjang</button>
        <button @click="removeFromCart(product)">Kurangi dari Keranjang</button>
      </div>
    </div>
    <div v-if="showCart" class="payment">
      <h2>Total Belanja: Rp {{ totalBiaya }}</h2>
      <button @click="bayar">Bayar</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        {
          id: 1,
          title: "Laptop Gaming",
          description: "Spesifikasi tinggi untuk gaming",
          price: 15000000,
          image: "PC.png",
        },
        {
          id: 2,
          title: "PC Gaming",
          description: "Custom PC gaming",
          price: 12000000,
          image: "PCN.png",
        },
        {
          id: 3,
          title: "PlayStation 5",
          description: "Konsol game terbaru",
          price: 8000000,
          image: "PS.png",
        },
        {
          id: 4,
          title: "FIFA 22 (Digital)",
          description: "Game sepakbola terkenal",
          price: 500000,
          image: "asik.png",
        },
      ],

      cartItems: [],
      showCart: false,
    };
  },
  computed: {
    formattedProducts() {
      return this.products.map((product) => {
        return {
          ...product,
          price: "Rp " + product.price.toLocaleString("id-ID"),
        };
      });
    },
    totalBiaya() {
      return this.cartItems
        .reduce((total, product) => total + product.price, 0)
        .toLocaleString("id-ID");
    },
  },
  methods: {
    addToCart(product) {
      this.cartItems.push(product);
    },
    removeFromCart(product) {
      const index = this.cartItems.indexOf(product);
      if (index !== -1) {
        this.cartItems.splice(index, 1);
      }
    },
    toggleCart() {
      this.showCart = !this.showCart;
    },
    bayar() {
      // Ganti '/payment' dengan path halaman pembayaran Anda
      this.$router.push("https://www.dana.id/");
    },
  },
};
</script>

<style>
/* CSS styling untuk header */
.header {
  display: flex;
  align-items: center;
}

.site-name {
  font-size: 24px;
  font-weight: bold;
  margin-left: 10px;
  color: #333;
}

/* Gaya CSS tambahan untuk navigasi bar */
nav {
  background: linear-gradient(180deg, #000 0%, #000 20%, #3498db 20%, #3498db);
  color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  position: relative;
}

nav ul {
  list-style: none;
  display: flex;
  gap: 20px;
}

nav a {
  text-decoration: none;
  color: #fff;
  font-weight: bold;
  transition: color 0.3s;
}

nav a:hover {
  color: #2196f3;
  border-bottom: 2px solid #2196f3;
}

/* Gaya CSS tambahan untuk keranjang */
.cart {
  display: flex;
  align-items: center;
  cursor: pointer;
}

.cart-icon {
  font-size: 24px;
}

.cart-total {
  margin-left: 10px;
  font-weight: bold;
  font-size: 16px;
}

/* Gaya CSS tambahan untuk produk */
.container {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-between;
  margin-top: 20px;
}

.product {
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 20px;
  margin: 10px;
  width: calc(33.33% - 20px);
  text-align: center;
}

.product h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.product img {
  margin: 0 auto;
  display: block;
}

.product p {
  font-size: 1rem;
  color: #666;
  margin-bottom: 10px;
}

.product strong {
  font-weight: bold;
}

.product button {
  background-color: #2196f3;
  color: #fff;
  border: none;
  padding: 5px 10px;
  cursor: pointer;
  margin-right: 5px;
}

.product button:hover {
  background-color: #1976d2;
}

/* Gaya CSS tambahan untuk pembayaran */
.payment {
  background-color: #fff;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 20px;
  text-align: center;
  margin-top: 20px;
}

.payment h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.payment button {
  background-color: #4caf50;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 1rem;
}

.payment button:hover {
  background-color: #45a049;
}
</style>
