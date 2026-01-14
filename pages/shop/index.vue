<script setup>
import ProductCard from '../../components/ProductCard.vue';
import SearchSortBar from '../../components/SearchSortBar.vue';

const search = ref('')
const sortByPrice = ref('relevance')
const filterByCategory= ref('all')

const products = ref([
        { id: 1, name: 'Wall-Mounted AC Unit 9k BTU', price: 699, inStock: true, category: 
        'Cooling', brand: 'CoolBreeze' },
        { id: 2, name: 'Ducted Heat Pump 16 kW', price: 2390, inStock: false, category: 
        'Heating', brand: 'ThermoMax' },
        { id: 3, name: 'Smart WiFi Thermostat', price: 199, inStock: true, category: 'Controls', brand: 
        'HomeSense' },
        { id: 4, name: 'HEPA Air Filter Cartridge', price: 49, inStock: true, category: 'Filtration', brand: 
        'PureAir' },
        { id: 5, name: 'Heat Recovery Ventilation Unit',price: 1499, inStock: true, category: 
        'Ventilation',brand: 'FreshFlow' },
        { id: 6, name: 'Insulated Flexible Duct 10m', price: 129, inStock: false, category: 
        'Ducting', brand: 'DuctPro' },
])

const filteredProducts = computed(() => {
        let productCopy = products.value
        const searchTerm = search.value?.toLowerCase().trim() || ''

        if (searchTerm) {
            productCopy = productCopy.filter(p => p.name.toLowerCase().includes(searchTerm))
        }

        if (sortByPrice.value === 'price-asc') {
            productCopy = [...productCopy].sort((a, b) => a.price - b.price)
        } else if (sortByPrice.value === 'price-desc') {
            productCopy = [...productCopy].sort((a, b) => b.price - a.price)
        }

        if (filterByCategory.value !== 'all') {
            productCopy = productCopy.filter(p => p.category === filterByCategory.value)
        }
        
        return productCopy
})
</script>
<template>
    <div class="px-6">
        <div class="border-b mx-auto py-8 text-center">
            <h1 class="text-lg font-bold text-gray-900 sm:text-2xl">
                Climate Control Products
            </h1>
            <p class="mt-2 text-xs text-gray-600 sm:text-sm">
                Browse our heating, cooling and ventilation products
            </p>
        </div>
        <SearchSortBar  
            v-model:search="search"
            v-model:sort="sortByPrice"/>

        <ProductCard 
            :products="filteredProducts"
            v-model:filter="filterByCategory"/>
    </div>
</template>