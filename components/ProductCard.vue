<script setup>
defineProps({
    products: {
        type: Array,
        required: true,
    }
})

const filter = defineModel('filter', { default: 'all' })

</script>
<template>
    <div class="flex justify-end sm:pr-2 p-2">
        <div class="w-full sm:w-56">
      <label class="sr-only" for="filter">Filter by</label>
      <select
        id="filter"
        v-model="filter"
        class="w-full rounded-md border border-gray-200 bg-white px-3 py-2 text-sm text-gray-900 shadow-sm outline-none focus:border-gray-400 focus:ring-2 focus:ring-gray-200"
      >
        <option value="all">All categories</option>
        <option value="Cooling">Cooling</option>
        <option value="Heating">Heating</option>
        <option value="Ventilation">Ventilation</option>
        <option value="Filtration">Filtration</option>
        <option value="Ducting">Ducting</option>
        <option value="Controls">Controls</option>
      </select>
    </div>
    </div>
    <div v-if="products.length > 0" class="mt-4 p-2 grid grid-cols-1 gap-x-4 gap-y-6 sm:grid-cols-2 lg:grid-cols-3 xl:gap-x-3">
      <div v-for="product in products" :key="product.id" class="group rounded-2xl border border-gray-300 bg-white shadow-sm transition hover:shadow-md">
          <NuxtLink :to='`/shop/${product.id}`'>
          <div class="flex flex-col">
              <div class="flex flex-col border-b p-3">
                  <h3 class="text-lg text-gray-700">
                  {{product.name}}
                  </h3>
                  <p class="mt-1 text-left font-semibold text-green-700">${{product.price}}</p>
              </div>
              <div class="flex justify-between p-2 border-b ">
                  <span class="inline-flex items-center rounded-full px-2.5 py-1 text-xs font-semibold "
                    :class="product.inStock ? 'bg-green-100 text-green-600' : 'bg-gray-100 text-gray-600'">
                        {{product.inStock ? "In stock" : "Out of stock"}} 
                  </span>
                  <div class="flex flex-col border-l-4 pl-2 p-2 border-purple-500">
                      <p class=" text-sm uppercase tracking-wide text-gray-400">Category</p>
                      <p class="text-xs font-semibold text-gray-700">{{ product.category }}</p>
                  </div>
                  <div class="flex flex-col border-l-4 pl-2 p-2 border-green-500">
                        <p class="text-sm uppercase tracking-wide text-gray-400">Brand</p>
                        <p class="text-xs font-semibold text-gray-700">{{product.brand}}</p>
                  </div>
            </div>
          </div>
          </NuxtLink>
          <div class="flex justify-center my-2">
              <button class="p-2 text-white border rounded-md text-sm disabled:bg-gray-300 disabled:text-gray-500 disabled:cursor-not-allowed bg-blue-600 hover:bg-blue-500"
                      :disabled="!product.inStock"> Add to cart
              </button>
          </div>
      </div>
    </div>
    <div v-else class="p-6 text-sm text-gray-600 italic">
      No products found for your search
    </div>
</template>