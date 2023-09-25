<template>
  <div class="p-4 border rounded-md">
    <!-- Availability Filter -->
    <div class="mb-4">
      <label class="flex items-center">
        <input type="checkbox" v-model="onlyAvailable" class="mr-2" />
        Show Only Available Products
      </label>
    </div>
    <!-- Brand Filter -->
    <div>
      <p class="font-bold mb-2">Filter by Brand:</p>
      <div class="flex space-x-4">
        <!-- Flex and space-x-4 classes added here -->
        <div v-for="brand in brands" :key="brand" class="mb-2">
          <label class="flex items-center">
            <input
              type="checkbox"
              :value="brand"
              v-model="selectedBrands"
              class="mr-2"
            />
            {{ brand }}
          </label>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    brands: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      onlyAvailable: false,
      selectedBrands: [],
    };
  },
  watch: {
    onlyAvailable(value) {
      this.$emit('filter-availability', value);
    },
    selectedBrands(value) {
      this.$emit('filter-brands', value);
    },
  },
};
</script>

<style scoped></style>
