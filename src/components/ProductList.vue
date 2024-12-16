<template>
  <v-container>
    <v-row>
      <v-col
        cols="12"
        sm="6"
        md="4"
        lg="3"
        v-for="product in products"
        :key="product.id"
      >
        <v-card class="ma-3">
          <v-img
            :src="product.image"
            class="white--text align-end"
            height="200px"
          ></v-img>
          <v-card-title>{{ product.title }}</v-card-title>
          <v-card-subtitle>Category: {{ product.category }}</v-card-subtitle>
          <v-card-subtitle>Price: ${{ product.price }}</v-card-subtitle>
          <v-card-actions>
            <v-btn color="primary" @click="$emit('add-to-cart', product)">
              Add to Cart
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'ProductList',
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
</style>
