<script setup>
import { ref } from 'vue';
const header = ref('App Lista de compras');
</script>

<template>
  <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem; /* Adjust the font-size value as per your desired size */
}
</style>
