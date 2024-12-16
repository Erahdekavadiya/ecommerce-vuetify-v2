<template>
  <v-app>
    <!-- Header -->
    <v-app-bar app color="primary" dark>
      <v-app-bar-title>E-Commerce Components</v-app-bar-title>
      <v-spacer></v-spacer>
      <v-btn icon @click="toggleCart">
        <v-icon>mdi-cart</v-icon>
      </v-btn>
    </v-app-bar>

    <!-- Cart Drawer -->
    <v-navigation-drawer
      v-model="isCartOpen"
      right
      temporary
      app
    >
      <v-toolbar flat color="primary" dark>
        <v-toolbar-title>Cart</v-toolbar-title>
        <v-spacer></v-spacer>
        <v-btn icon @click="toggleCart">
          <v-icon>mdi-close</v-icon>
        </v-btn>
      </v-toolbar>
      <Cart :cartItems="cartItems" @remove-item="removeFromCart" @clearcart="clearcartitems"/>
    </v-navigation-drawer>

    <!-- Main Content -->
    <v-container>
      <v-row>
        <v-col cols="12" md="3">
          <!-- Product Filter Component -->
          <ProductFilter 
            :categories="categories" 
            :maxPrice="maxPrice" 
            @filterChanged="updateFilter" 
          />
        </v-col>
        <v-col cols="12" md="9">
          <!-- Product List Component -->
          <ProductList 
            :products="filteredProducts" 
            @add-to-cart="addToCart" 
          />
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
import axios from 'axios';
import ProductFilter from './components/ProductFilter.vue';
import ProductList from './components/ProductList.vue';
import Cart from './components/Cart.vue';

export default {
  name: 'App',
  components: {
    ProductFilter,
    ProductList,
    Cart,
  },
  data() {
    return {
      products: [], // All products
      cartItems: [], // Cart items
      categories: [], // Product categories
      maxPrice: 0, // Maximum price from API
      filter: {
        category: 'all'
      },
      isCartOpen: false, // Cart drawer visibility
    };
  },
  computed: {
    // Filtered products computed function
    filteredProducts() {
      return this.products.filter((product) => {
        const matchesCategory =
          this.filter.category === 'all' || product.category === this.filter.category;
        return matchesCategory;
      });
    },
  },
  methods: {
    async fetchProducts() {
      try {
        const response = await axios.get('https://fakestoreapi.com/products');
        this.products = response.data;

        // Dynamically set categories and max price
        this.categories = ['all', ...new Set(this.products.map((product) => product.category))];
        this.maxPrice = Math.ceil(
          Math.max(...this.products.map((product) => parseFloat(product.price)))
        );
      } catch (error) {
        console.error('Error fetching products:', error);
      }
    },
    updateFilter(newFilter) {
      this.filter = newFilter;
    },
    addToCart(product) {
      const existingItem = this.cartItems.find((item) => item.id === product.id);
      if (existingItem) {
        existingItem.quantity += 1;
      } else {
        this.cartItems.push({ ...product, quantity: 1 });
      }
      this.isCartOpen = true;
    },
    removeFromCart(item) {
      this.cartItems = this.cartItems.filter((cartItem) => cartItem.id !== item.id);
    },
    toggleCart() {
      this.isCartOpen = !this.isCartOpen;
    },
    clearcartitems(){
      this.cartItems = [];
    }
  },
  created() {
    this.fetchProducts();
  },
};
</script>
