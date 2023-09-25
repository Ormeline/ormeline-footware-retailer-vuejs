<template>
  <div class="container mx-auto px-4 py-8">
    <!-- Retailer Logo -->
    <div class="mb-8 text-center">
      <h1 class="text-2xl font-bold">Ormeline's Trainer Shop</h1>
    </div>

    <!-- Filters and Sorting -->
    <div
      class="
        flex flex-col
        space-y-3
        mb-6
        md:flex-row md:space-y-0 md:justify-between
      "
    >
      <FilterCheckbox
        :brands="brands"
        @filter-availability="filterAvailability"
        @filter-brands="filterBrands"
      ></FilterCheckbox>
      <SortingDropdown @sort-changed="changeSort"></SortingDropdown>
    </div>

    <!-- Product Counter -->
    <p class="mb-4">Showing {{ filteredProducts.length }} products</p>

    <!-- Product Grid -->
    <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
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
import products from './data/products.json';

export default {
  components: {
    ProductCard,
    FilterCheckbox,
    SortingDropdown,
  },
  data() {
    return {
      products,
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
