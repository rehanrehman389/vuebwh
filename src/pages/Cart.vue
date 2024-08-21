<!-- src/components/Cart.vue -->
<template>
  <div class="w-1/4 p-4">
    <h2 class="text-xl font-semibold mb-4">Cart</h2>
    <div v-if="cart.length === 0" class="text-gray-500">
      Your cart is empty.
    </div>
    <div v-else>
      <div v-for="item in cart" :key="item.product.id" class="mb-4">
        <div class="flex justify-between">
          <div>
            <h3 class="text-lg font-semibold">{{ item.product.name }}</h3>
            <p class="text-gray-500">{{ item.product.price }}</p>
            <p class="text-gray-500">Quantity: {{ item.quantity }}</p>
          </div>
          <button @click="removeFromCart(item.product.id)" class="bg-red-500 text-white py-1 px-2 rounded-lg hover:bg-red-600">
            Remove
          </button>
        </div>
      </div>
      <button @click="orderItems" class="bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-600 mt-4">
        Order
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Cart',
  props: {
    cart: Array
  },
  methods: {
    removeFromCart(productId) {
      this.$emit('remove-from-cart', productId);
    },
    orderItems() {
      console.log('Order placed for the following items:', this.cart);
    }
  }
}
</script>

<style scoped>
/* Add any additional styles if needed */
</style>
