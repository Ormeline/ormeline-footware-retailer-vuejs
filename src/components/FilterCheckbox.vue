<template>
  <!-- Availability Filter -->
    <label class="flex items-center text-sm">
      <input type="checkbox" v-model="onlyAvailable" class="mr-2" />
      Show Only Available Products
    </label>
  </div>
  <!-- Brand Filter -->
  <div>
    <p class="font-bold mb-2 text-sm">Filter by Brand:</p>
    <div class="grid md:grid-cols-5 grid-cols-1 gap-2">
      <div v-for="brand in brands" :key="brand" class="mb-2">
        <label class="flex items-center text-xs">
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
  <div>
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
