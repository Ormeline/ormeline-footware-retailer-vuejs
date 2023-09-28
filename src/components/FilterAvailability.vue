<template>
  <!-- Availability Filter -->
    <label class="flex items-center text-sm">
      <input type="checkbox" v-model="onlyAvailable" class="mr-2" />
      Show Only Available Products
    </label>
  </div>
</template>

<script>
export default {
  data() {
    return {
      onlyAvailable: false,
    };
  },
  emits: 'filter-availability',
  watch: {
    onlyAvailable(value) {
      this.$emit('filter-availability', value);
    },
  },
};
</script>

<style scoped></style>
