<script lang="js">
import axios from 'axios';
export default {
  data() {
    return {
      productList: [],
      searchQuery: '',
      currentPage: 1,
      itemsInPage: 5,
      filter: []
    };
  },
  computed: {
    totalPagesForProducts() {
      return Math.ceil(this.filter.length / this.itemsInPage);
    },
    paginatedAllProducts() {
      const startIndex = (this.currentPage - 1) * this.itemsInPage;
      const endIndex = startIndex + this.itemsInPage;
      return this.filter.slice(startIndex, endIndex);
    }
  },
  methods: {
    previousPageForProducts() {
      if (this.currentPage > 1) {
        this.currentPage--;
      }
    },
    nextPageForProducts() {
      if (this.currentPage < this.totalPagesForProducts) {
        this.currentPage++;
      }
    },
    firstPageForProducts() {
      if (this.currentPage > 1) {
        this.currentPage = 1;
      }
    },
    lastPageForProducts() {
      if (this.currentPage < this.totalPagesForProducts) {
        this.currentPage = this.totalPagesForProducts
      }
    },

    searchForProducts() {
      this.filter = this.productList.filter(product =>
          product.id.toString().toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          product.title.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          product.price.toString().toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          product.category.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          product.rating.toString().toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          product.brand.toLowerCase().includes(this.searchQuery.toLowerCase()) ||
          product.description.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
      this.currentPage = 1;
    }
  },

  async mounted() {
    try {
      const response = await axios.get('https://dummyjson.com/products');
      this.productList = response.data.products;
      this.filter = this.productList;
    } catch (err) {
      console.error('Error fetching to API:', err);
    }
  }
};
</script>
<template>
  <div>
    <h1 class="text-2xl m-5 text-black-500">Список продуктів</h1>
    <input type="text" v-model="searchQuery" @input="searchForProducts" placeholder="Пошук продукту" class="bg-gray-200 py-2 px-4 rounded-lg focus:outline-none focus:shadow-outline w-50" style="margin-bottom: 10px; color:black;">
    <table class="w-full border-collapse">
      <thead>
      <tr>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">id</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Назва</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Ціна</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Категорія</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Оцінка</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Бренд</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Фото</th>
        <th class="bg-gray-100 border border-gray-300 py-2 px-4 text-left">Опис</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="product in paginatedAllProducts" :key="product.id" class="border border-gray-300 hover:bg-gray-100">
        <td class="border border-gray-300 py-2 px-4">{{ product.id }}</td>
        <td class="border border-gray-300 py-2 px-4">{{ product.title }}</td>
        <td class="border border-gray-300 py-2 px-4">{{ product.price }}</td>
        <td class="border border-gray-300 py-2 px-4">{{ product.category }}</td>
        <td class="border border-gray-300 py-2 px-4" :style="{ color: product.rating < 4.5 ? 'red' : 'green' }">{{ product.rating }}</td>
        <td class="border border-gray-300 py-2 px-4">{{ product.brand }}</td>
        <td class="border border-gray-300 py-2 px-4">
          <img :src="product.thumbnail" alt="Product Thumbnail">
        </td>
        <td class="border border-gray-300 py-2 px-4">{{ product.description }}</td>

      </tr>
      </tbody>
    </table>
    <button @click="firstPageForProducts" :disabled="currentPage === 1" class="bg-blue-500 my-5 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mr-2">
      <<
    </button>
    <button @click="previousPageForProducts" :disabled="currentPage === 1" class="bg-blue-500 my-5 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mr-2">
      <
    </button>
    <span class="text-gray-500 my-5"> {{ currentPage }} з {{ totalPagesForProducts }}</span>
    <button @click="nextPageForProducts" :disabled="currentPage === totalPagesForProducts" class="bg-blue-500 my-5 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded ml-2">
      >
    </button>
    <button @click="lastPageForProducts" :disabled="currentPage === totalPagesForStudent" class="bg-blue-500 my-5 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded ml-2">
      >>
    </button>
  </div>
</template>

<style scoped>
img {
  width: 100px !important;
  height: 100px !important;
}
</style>