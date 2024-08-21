<!-- src/components/ProductList.vue -->
<template>
    <div class="container mx-auto p-4 flex">
      <FilterSidebar @filter-changed="filterProducts" class="w-1/4" />
      <div class="w-3/4">
        <h1 class="text-2xl font-bold mb-4">Product List</h1>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
          <ProductCard
            v-for="product in filteredProducts"
            :key="product.id"
            :product="product"
            @add-to-cart="addToCart"
          />
        </div>
      </div>
      <Cart :cart="cart" @remove-from-cart="removeFromCart" />
    </div>
  </template>
  
  <script>
  import ProductCard from './ProductCard.vue';
  import FilterSidebar from './FilterSidebar.vue';
  import Cart from './Cart.vue';
  
  export default {
    name: 'ProductList',
    components: {
      ProductCard,
      FilterSidebar,
      Cart
    },
    data() {
      return {
        products: [
          {
            id: 1,
            name: 'Apple iPhone XR (64GB) - Black (6 GB RAM)',
            category: 'Products',
            price: '₹36,900.00',
            discountedPrice: '₹31,365.00',
            discount: 15,
            stock: 10,
            image: 'https://m.media-amazon.com/images/I/61bK6PMOC3L._AC_UF1000,1000_QL80_.jpg',
            rating: 1
          },
          {
            id: 2,
            name: 'Apple iPhone Mobile 11 Pro Max 64GB (Midnight Green, 6GB RAM)',
            category: 'Products',
            price: '₹4,500.00',
            discountedPrice: '₹4,050.00',
            discount: 10,
            stock: 5,
            image: 'https://cdn.mos.cms.futurecdn.net/yDn3ZSXu9eSBxmXQDZ4PCF-1200-80.jpg',
            rating: 1
          },
          {
            id: 3,
            name: 'Apple iPhone 11 Pro (64GB)',
            category: 'Mobiles',
            price: '₹99,900.00',
            discountedPrice: '₹99,900.00',
            discount: 0,
            stock: 0,
            image: 'https://via.placeholder.com/150',
            rating: 1
          }
        ],
        filteredProducts: [],
        cart: JSON.parse(localStorage.getItem('cart')) || []
      };
    },
    methods: {
      filterProducts(selectedCategories) {
        if (selectedCategories.length === 0) {
          this.filteredProducts = this.products;
        } else {
          this.filteredProducts = this.products.filter(product =>
            selectedCategories.includes(product.category)
          );
        }
      },
      addToCart(product) {
        const cartItem = this.cart.find(item => item.product.id === product.id);
        if (cartItem) {
          cartItem.quantity++;
        } else {
          this.cart.push({ product, quantity: 1 });
        }
        localStorage.setItem('cart', JSON.stringify(this.cart));
      },
      removeFromCart(productId) {
        this.cart = this.cart.filter(item => item.product.id !== productId);
        localStorage.setItem('cart', JSON.stringify(this.cart));
      }
    },
    mounted() {
      this.filteredProducts = this.products;
    }
  };
  </script>
  
  <style scoped>
  /* Add any additional styles if needed */
  </style>
  