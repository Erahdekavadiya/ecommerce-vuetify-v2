<template>
  <v-container>
    <v-row>
      <v-col>
        <v-list two-line>
          <template v-for="item in cartItems"  :key="item.id">
            <v-list-item>
              <v-list-item-avatar>
                <v-img :src="item.image"></v-img>
              </v-list-item-avatar>

              <v-list-item-content>
                <v-list-item-title>{{ item.title }}</v-list-item-title>
                <v-list-item-subtitle>
                  ${{ item.price }} x {{ item.quantity }} = ${{ item.price * item.quantity }}
                </v-list-item-subtitle>
              </v-list-item-content>

              <v-list-item-action>
                <v-btn icon color="red" @click="removeFromCart(item)">
                  <v-icon>mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
            </v-list-item>
            <v-divider></v-divider>
          </template>
        </v-list>

        <v-card-actions v-if="cartItems.length > 0">
          <v-btn color="primary" block @click="checkoutclick">Checkout</v-btn>
        </v-card-actions>
        <v-card-actions v-if="cartItems.length === 0">
          <p>Your cart is empty!</p>
        </v-card-actions>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'Cart',
  props: {
    cartItems: {
      type: Array,
      required: true,
    },
  },
  methods: {
    removeFromCart(item) {
      this.$emit('remove-item', item);
    },
    checkoutclick(){
      alert("Thanks for checkout!");
      this.$emit('clearcart');
    }
  },
};
</script>

<style scoped>
</style>
