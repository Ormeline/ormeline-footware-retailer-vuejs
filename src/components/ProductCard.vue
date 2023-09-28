<template>
  <div
    class="
      p-4
      border
      rounded-md
      shadow-md
      hover:shadow-lg
      transition-shadow
      bg-white
      duration-300
    "
  >
    <img
      :src="product.image"
      alt="Product Image"
      class="object-cover mb-4 w-full"
    />
    <h2 class="font-bold text-sm lg:text-lg mb-2">
      {{ product.brand }} - {{ product.name }}
    </h2>
    <p class="text-sm lg:text-lg font-semibold mb-2">
      £{{ product.price.toFixed(2) }}
    </p>
    <p v-if="!product.isAvailable" class="text-sm lg:text-xl text-red-600">
      Not In Stock
    </p>
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
