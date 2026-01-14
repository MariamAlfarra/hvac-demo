<script setup>
const route = useRoute()
</script>

<template>
  <div class="p-6 text-center">
    <p> Product {{ route.params.id }} </p>
  </div>
</template>