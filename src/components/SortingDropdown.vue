<template>
  <div class="inline-block text-left">
    <div>
      <button
        @click="open = !open"
        type="button"
        class="font-bold rounded-md text-sm"
      >
        Sort By:
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

    <div v-if="open" class="absolute rounded-md shadow-lg">
      <div class="rounded-md bg-white shadow-xs">
        <div class="py-1" role="menu" aria-orientation="vertical">
          <button
            v-for="option in sortOptions"
            :key="option.value"
            @click="setSort(option.value)"
            class="
              block
              px-4
              py-2
              text-sm
              leading-5
              text-gray-700
              hover:bg-gray-100
              focus:outline-none
              text-left
              w-full
            "
            role="menuitem"
          >
            {{ option.label }}
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
      sortOptions: [
        { value: 'price-asc', label: 'Price: Low to High' },
        { value: 'price-desc', label: 'Price: High to Low' },
        { value: 'relevance', label: 'Relevance' },
      ],
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
