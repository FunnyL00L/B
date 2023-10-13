<template>
  <div id="second">
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
        <li><a href="">Jual Second</a></li>
      </ul>
      <div class="cart" @click="toggleCart">
        <div class="cart-icon">🛒</div>
        <div class="cart-total">Keranjang ({{ cartItems.length }})</div>
      </div>
    </nav>
    <div class="container">
      <!-- Form untuk input data -->
      <div class="product-form">
        <h2>Input Data Barang</h2>
        <input v-model="newProduct.name" type="text" placeholder="Nama Barang" />
        <input v-model="newProduct.price" type="text" placeholder="Harga Barang" />
        <select v-model="newProduct.condition">
          <option value="lecet">Lecet</option>
          <option value="mulus">Mulus</option>
        </select>
        <input v-model="newProduct.usage" type="text" placeholder="Lama Penggunaan" />
        <button @click="saveProduct">Simpan</button>
      </div>
      <!-- Daftar Produk -->
      <div class="product" v-for="product in formattedProducts" :key="product.id">
        <h2>{{ product.title }}</h2>
        <p>{{ product.description }}</p>
        <p><strong>{{ product.price }}</strong></p>
        <button @click="addToCart(product)">Tambah ke Keranjang</button>
        <button @click="removeFromCart(product)">Kurangi dari Keranjang</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        // Data produk yang ada
      ],
      cartItems: [],
      showCart: false,
      newProduct: {
        name: "",
        price: "",
        condition: "lecet",
        usage: "",
      },
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
    saveProduct() {
      if (this.newProduct.name && this.newProduct.price && this.newProduct.usage) {
        this.products.push({
          id: this.products.length + 1,
          title: this.newProduct.name,
          description: `Status: ${this.newProduct.condition}, Lama Penggunaan: ${this.newProduct.usage}`,
          price: parseFloat(this.newProduct.price),
          image: "", // Tambahkan path gambar jika ada
        });
        this.newProduct = {
          name: "",
          price: "",
          condition: "lecet",
          usage: "",
        };
      }
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

.product-form {
  background-color: #f0f0f0;
  border: 1px solid #ddd;
  border-radius: 5px;
  padding: 20px;
  margin: 10px;
  width: calc(33.33% - 20px);
  text-align: center;
}

.product-form h2 {
  font-size: 1.5rem;
  margin-bottom: 10px;
}

.product-form input,
.product-form select {
  width: 100%;
  padding: 10px;
  margin-bottom: 10px;
}

.product-form button {
  background-color: #4caf50;
  color: #fff;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  font-size: 1rem;
}

.product-form button:hover {
  background-color: #45a049;
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
