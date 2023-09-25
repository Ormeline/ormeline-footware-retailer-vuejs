<template>
  <div class="app" ref="app-container">
    <div class="task">
      <h2>Welcome to the Hullabalook Technical Assessment</h2>
      <p>
        You are provided with a set of products and are required to create a
        products listing page for a footwear retailer.<br />
        Write functionality and styling to:
      </p>
      <ol>
        <li>Lay out all products in a responsive product grid</li>
        <li>Create a filter toggle that shows only available products</li>
        <li>
          Create a checkbox brand filter that shows only toggled brand products
        </li>
        <li>Add a counter for the number of resulting products</li>
        <li>
          Create a dropdown to sort all products into ascending or descending
          price order
        </li>
        <li>
          Add an option to sort all products by relevance - with all available
          products shown first in ascending rank order, then all unavailable
          products in ascending rank order.
        </li>
      </ol>
      <p>
        You will be assessed on both behaviour and design. Don't spend more than
        2 hours on this.
      </p>

      <h3>Instructions</h3>
      <p>
        To start, fork
        <a
          class="link"
          href="https://stackblitz.com/edit/vue-hulla-ta"
          target="_blank"
          >this</a
        >
        project and set the project name to include your name. When you're
        finished, connect this to your GitHub account, push the changes and
        email the links to the repo and this project back to us.
        <br />
        If you wish to continue past the allocated time, please create another
        fork.
      </p>
      <hr />
    </div>

    <div class="filters">
      <h3>Filters</h3>
      <div></div>
    </div>

    <div class="product-grid">
      <ProductGridItem :product="products[0]" />
      <ProductGridItem :product="products[1]" />
    </div>
  </div>
</template>

<script>
import ProductGridItem from './components/ProductGridItem.vue';
import products from './data/products.json';

export default {
  name: 'App',
  components: {
    ProductGridItem,
  },
  data() {
    return {
      products,
    };
  },
};
</script>

<style>
.app {
  max-width: 1024px;
  margin: 0 auto;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  color: #606569;
}

.link {
  color: #3a7f71;
}
</style>
