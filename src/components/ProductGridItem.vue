<template>
  <div class="product-grid-item">
    <img class="product-image" :src="product.image" />
    <p class="product-name">{{ product.name }}</p>
  </div>
</template>

<script>
export default {
  name: 'ProductGridItem',
  props: {
    product: { type: Object, required: true, default: () => ({}) },
  },
};
</script>
