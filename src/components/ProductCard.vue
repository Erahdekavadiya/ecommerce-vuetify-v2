<template>
  <v-card>
    <v-img :src="product.image" height="200px" />
    <v-card-title>{{ product.title }}</v-card-title>
    <v-card-subtitle>${{ product.price }}</v-card-subtitle>
    <v-card-text>
      <p>{{ product.description }}</p>
    </v-card-text>
    <v-card-actions>
      <v-btn @click="addToCart" color="primary">Add to Cart</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: 'ProductCard',
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.product);
    },
  },
};
</script>

<style scoped>
</style>
