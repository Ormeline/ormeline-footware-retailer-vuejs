<template>
  <div class="relative inline-block text-left">
    <div>
      <button
        @click="open = !open"
        type="button"
        class="bg-primary text-white px-4 py-2 rounded-md"
      >
        Sort
        <svg
          class="w-5 h-5 inline-block ml-2"
          fill="none"
          stroke="currentColor"
          viewBox="0 0 24 24"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            strokeLinecap="round"
            strokeLinejoin="round"
            strokeWidth="2"
            d="M19 9l-7 7-7-7"
          ></path>
        </svg>
      </button>
    </div>

    <div
      v-if="open"
      class="origin-top-right absolute right-0 mt-2 w-56 rounded-md shadow-lg"
    >
      <div class="rounded-md bg-white shadow-xs">
        <div class="py-1" role="menu" aria-orientation="vertical">
          <button
            @click="setSort('price-asc')"
            class="
              block
              px-4
              py-2
              text-sm
              leading-5
              text-gray-700
              hover:bg-gray-100
              focus:outline-none
            "
            role="menuitem"
          >
            Price: Low to High
          </button>
          <button
            @click="setSort('price-desc')"
            class="
              block
              px-4
              py-2
              text-sm
              leading-5
              text-gray-700
              hover:bg-gray-100
              focus:outline-none
            "
            role="menuitem"
          >
            Price: High to Low
          </button>
          <button
            @click="setSort('relevance')"
            class="
              block
              px-4
              py-2
              text-sm
              leading-5
              text-gray-700
              hover:bg-gray-100
              focus:outline-none
            "
            role="menuitem"
          >
            Relevance
          </button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      open: false,
    };
  },
  methods: {
    setSort(value) {
      this.$emit('sort-changed', value);
      this.open = false;
    },
  },
};
</script>

<style scoped></style>
