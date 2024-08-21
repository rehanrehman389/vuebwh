<template>
  <div class="container">
    <h3 class="text-3xl font-bold mb-4 text-center">Shop from nearest stores</h3>
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
      <div v-for="seller in sellers" :key="seller.name" class="p-4 bg-white shadow-md rounded-lg flex items-center transition-transform hover:-translate-y-1">
        <img :src="seller.seller_logo" alt="Seller Logo" class="w-16 h-16 object-cover rounded-lg mr-4">
        <div class="flex-1">
          <h3 class="text-lg font-semibold">{{ seller.seller_name }}</h3>
          <p class="text-gray-600">{{ seller.address || 'No address available' }}</p>
        </div>
      </div>
    </div>
    <Button
      :variant="'solid'"
      theme="gray"
      size="lg"
      label="Button"
      :loading="false"
      :loadingText="null"
      :disabled="false"
      :link="null"
      @click="loadMore"
    >
    Load More
    </Button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      sellers: [],
      start: 0,
      isLoading: false,
    };
  },
  async mounted() {
    await this.fetchData();
  },
  methods: {
    async fetchData() {
      const url = 'https://sit.mytra.money/api/method/mytra_money_internal.individuals.api.controller.get_ondc_sellers';
      const headers = {
        'Content-Type': 'application/json',
        'Cookie': 'full_name=Guest; sid=Guest; system_user=no; user_id=Guest; user_image=',
      };
      const body = JSON.stringify({
        user: 'harsh.agrawal1991@gmail.com',
        params: {
          address: 'Harsh Agrawal-Billing-1',
          start: this.start,
        },
      });

      try {
        this.isLoading = true;
        const response = await fetch(url, {
          method: 'POST',
          headers: headers,
          body: body,
        });

        if (!response.ok) {
          throw new Error(`HTTP error! status: ${response.status}`);
        }

        const data = await response.json();
        this.sellers = [...this.sellers, ...data.message.map(seller => ({
          name: seller.name,
          seller_name: seller.seller_name,
          seller_logo: seller.seller_logo,
          address: seller.serviceable_city || 'No address available',
        }))];
      } catch (error) {
        console.error('Error fetching data:', error);
      } finally {
        this.isLoading = false;
      }
    },
    loadMore() {
      this.start += 20;
      this.fetchData();
    },
  },
};
</script>
