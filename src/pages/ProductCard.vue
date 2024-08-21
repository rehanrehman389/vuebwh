<template>
    <div class="border rounded-lg overflow-hidden shadow-md">
      <div class="relative">
        <div class="absolute top-2 right-2 flex items-center">
          <span v-if="product.stock > 0" class="bg-red-100 text-red-600 rounded-full p-2 mr-2">
            <i class="fas fa-heart"></i>
          </span>
          <span v-if="product.stock > 0" class="bg-blue-500 text-white rounded-full w-8 h-8 flex items-center justify-center">
            {{ product.rating }}
          </span>
        </div>
        <img :src="product.image" alt="" class="w-full h-48 object-cover mb-4 rounded-t-lg">
      </div>
      <div class="p-4">
        <h2 class="text-lg font-semibold mb-2">{{ product.name }}</h2>
        <p class="text-gray-500 mb-1">{{ product.category }}</p>
        <div class="mb-2">
          <span class="text-lg font-bold text-black">{{ product.discountedPrice }}</span>
          <span v-if="product.discount" class="line-through text-gray-500 ml-2">{{ product.price }}</span>
          <span v-if="product.discount" class="text-green-500 ml-2">{{ product.discount }}% OFF</span>
        </div>
        <p v-if="product.stock > 0" class="text-green-500 mb-2">In stock</p>
        <p v-else class="text-red-500 mb-2">Out of stock</p>
        <button
          :class="product.stock > 0 ? 'bg-blue-500 text-white' : 'bg-gray-500 text-white cursor-not-allowed'"
          :disabled="product.stock <= 0"
          @click="addToCart(product)"
          class="py-2 px-4 rounded-lg hover:bg-blue-600 w-full"
        >
          {{ product.stock > 0 ? 'Add to Cart' : 'Out of stock' }}
        </button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ProductCard',
    props: {
      product: Object
    },
    methods: {
      addToCart(product) {
        if (product.stock > 0) {
          this.$emit('add-to-cart', product);
        }
      }
    }
  }
  </script>
  
  <style scoped>
  /* Additional styles for the product card */
  .border {
    border: 1px solid #e2e8f0; /* Light border color */
  }
  .rounded-lg {
    border-radius: 0.5rem; /* Rounded corners */
  }
  .overflow-hidden {
    overflow: hidden; /* Ensures content doesn't overflow rounded corners */
  }
  .shadow-md {
    box-shadow: 0 4px 6px -1px rgba(0, 0, 0, 0.1), 0 2px 4px -1px rgba(0, 0, 0, 0.06); /* Material design shadow */
  }
  .absolute {
    position: absolute;
  }
  .relative {
    position: relative;
  }
  </style>
  