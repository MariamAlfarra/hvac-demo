<script setup>
const search = defineModel('search', { default: '' })
const sort = defineModel('sort', { default: 'relevance' })

</script>
<template>
   <div class="flex flex-col gap-3 sm:flex-row sm:items-center p-2 mt-2">
    <div class="relative flex-1">
      <input
        v-model="search"
        type="text"
        class="w-full rounded-lg border border-gray-200 bg-white px-3 py-2 text-sm text-gray-900 placeholder:text-gray-400 shadow-sm outline-none focus:border-gray-400 focus:ring-2 focus:ring-gray-200"
        placeholder="Search for products"
      />
    </div>
    <div class="w-full sm:w-56">
      <label class="sr-only" for="sort">Sort by</label>
      <select
        id="sort"
        v-model="sort"
        class="w-full rounded-md border border-gray-200 bg-white px-3 py-2 text-sm text-gray-900 shadow-sm outline-none focus:border-gray-400 focus:ring-2 focus:ring-gray-200"
      >
        <option value="relevance">Sort: Relevance</option>
        <option value="price-asc">Price: Low → High</option>
        <option value="price-desc">Price: High → Low</option>
      </select>
    </div>
  </div>
</template>