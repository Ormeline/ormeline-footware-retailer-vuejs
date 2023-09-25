<template>
  <div
    class="
      p-4
      border
      rounded-md
      shadow-md
      hover:shadow-lg
      transition-shadow
      duration-300
    "
  >
    <img
      :src="product.image"
      alt="Product Image"
      class="w-full h-96 object-cover mb-4"
    />
    <h2 class="font-bold text-xl mb-2">
      {{ product.brand }} - {{ product.name }}
    </h2>
    <p class="text-primary font-semibold mb-2">
      £{{ product.price.toFixed(2) }}
    </p>
    <p v-if="!product.isAvailable" class="text-red-600">Not In Stock</p>
  </div>
</template>

<script>
export default {
  props: {
    product: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped></style>
