<template>
  <div class="container mx-auto px-4 py-4 bg-green-50">
    <!-- Retailer Logo -->
    <div class="mb-4 text-center">
      <h1 class="text-xl font-bold">Footwear Retailer</h1>
    </div>

    <!-- Filters and Sorting -->
    <div class="px-4 pt-4 rounded border bg-white">
      <div class="flex flex-col mb-4 space-y-5">
        <FilterCheckbox
          :brands="brands"
          @filter-availability="filterAvailability"
          @filter-brands="filterBrands"
        ></FilterCheckbox>
        <SortingDropdown @sort-changed="changeSort"></SortingDropdown>
      </div>
    </div>

    <!-- Product Counter -->
    <p class="my-4 text-left">Showing {{ filteredProducts.length }} products</p>

    <!-- Product Grid -->
    <div class="grid grid-cols-1 md:grid-cols-3 lg:grid-cols-5 gap-8">
      <ProductCard
        v-for="product in sortedProducts"
        :key="product.name"
        :product="product"
      ></ProductCard>
    </div>
  </div>
</template>

<script>
import ProductCard from './components/ProductCard.vue';
import FilterCheckbox from './components/FilterCheckbox.vue';
import SortingDropdown from './components/SortingDropdown.vue';
import importedProducts from './data/products.json';

export default {
  components: {
    ProductCard,
    FilterCheckbox,
    SortingDropdown,
  },
  data() {
    return {
      products: importedProducts,
      onlyAvailable: false,
      selectedBrands: [],
      sortOption: 'price-asc',
    };
  },
  computed: {
    brands() {
      // Extract unique brands from products
      return [...new Set(this.products.map((product) => product.brand))];
    },
    filteredProducts() {
      // Filter products based on availability and selected brands
      return this.products.filter((product) => {
        return (
          (this.onlyAvailable ? product.isAvailable : true) &&
          (this.selectedBrands.length
            ? this.selectedBrands.includes(product.brand)
            : true)
        );
      });
    },
    sortedProducts() {
      // Sort the filtered products based on the selected sort option
      if (this.sortOption === 'price-asc') {
        return [...this.filteredProducts].sort((a, b) => a.price - b.price);
      } else if (this.sortOption === 'price-desc') {
        return [...this.filteredProducts].sort((a, b) => b.price - a.price);
      } else if (this.sortOption === 'relevance') {
        return [...this.filteredProducts].sort((a, b) => {
          if (a.isAvailable && !b.isAvailable) return -1;
          if (!a.isAvailable && b.isAvailable) return 1;
          return a.rank - b.rank;
        });
      }
      return this.filteredProducts;
    },
  },
  methods: {
    filterAvailability(value) {
      this.onlyAvailable = value;
    },
    filterBrands(brands) {
      this.selectedBrands = brands;
    },
    changeSort(value) {
      this.sortOption = value;
    },
  },
};
</script>

<style scoped></style>
