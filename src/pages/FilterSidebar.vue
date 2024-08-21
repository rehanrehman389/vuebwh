<template>
    <div class="w-1/4 p-4">
      <h2 class="text-xl font-semibold mb-4">Filters</h2>
      <div class="mb-4">
        <h3 class="text-lg font-semibold mb-2">Item Group</h3>
        <div v-for="category in categories" :key="category" class="mb-2">
          <input
            type="checkbox"
            :id="category"
            :value="category"
            v-model="selectedCategories"
            class="mr-2"
          />
          <label :for="category">{{ category }}</label>
        </div>
      </div>
      <button @click="applyFilter" class="bg-blue-500 text-white py-2 px-4 rounded-lg hover:bg-blue-600">
        Apply Filter
      </button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'FilterSidebar',
    data() {
      return {
        categories: [
          'Accessories',
          'Mobile Services',
          'Laboratory',
          'Services',
          'Mobiles',
          'Furniture',
          'Products',
          'Test A'
        ],
        selectedCategories: []
      };
    },
    methods: {
      applyFilter() {
        this.$emit('filter-changed', this.selectedCategories);
      }
    }
  };
  </script>
  
  <style scoped>
  /* Add any additional styles if needed */
  </style>
  