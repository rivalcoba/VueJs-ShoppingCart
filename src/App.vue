<script setup>
import { ref } from 'vue';
// Modo edición
const editing = ref(false);
// Funcion que alterna el valor de la variable editing
const doEdit = (edit)=>{
  editing.value = edit;
  // Limpiando la entrada de texto
  // en caso de que se oculte o muestre
  // el formulario
  newItem.value = "";
  newItemHighPriority.value = false;
};

const header = ref('App Lista de compras');
const items = ref([
  {id: 1, label: '10 bolillos', purchased: true, highPriority: true },
  {id: 2, label: '1 lata de frijoles', purchased: false, highPriority: true },
  {id: 3, label: '2 lata de atún', purchased: true, highPriority: false }
]);
const newItem = ref('');
const newItemHighPriority = ref(false);
// Metodo para agregar nuevos elementos a la lista
const saveItem = () => {
  items.value.push({ 
    id: items.value.length + 1, 
    label: newItem.value,
    highPriority: newItemHighPriority.value
  });
  // Reiniciendo la entrada de texto
  newItem.value = "";
  newItemHighPriority.value = false;
};
// Alternando estado de compra del item
const togglePurchased = (item) => {
  item.purchased = !item.purchased;
};
</script>

<template>
  <div class="header">
    <h1> <i class="material-icons shopping-cart-icon">local_mall</i> {{ header }}</h1>
    <button v-if="editing" @click="doEdit(false)" class="btn">Cancel</button>
    <button v-else @click="doEdit(true)" class="btn btn-primary">Add Item</button>
  </div>
  <!-- Agrupando Entradas de usuario -->
  <form class="add-item form" v-if="editing" v-on:submit.prevent="saveItem">
    <!-- Entrada de texto -->
    <input 
      type="text" 
      placeholder="Add Item" 
      v-model.trim="newItem">
    <!-- Radio Buttons -->
    <label><input type="checkbox" v-model="newItemHighPriority">Alta Prioridad</label>
    <!-- Boton -->
    <button :disabled="newItem.length === 0" 
      class="btn btn-primary">
      Salvar Articulo
    </button>
  </form>
  <!-- Lista -->
  <ul>
    <li v-for="({ id, label, purchased, highPriority }, index) in items" 
      :class="{strikeout: purchased, priority: highPriority}"
      @click="togglePurchased(items[index])"
      v-bind:key="id">
      🔹 {{ label }}
    </li>
  </ul>
  <p v-if="items.length === 0">🥀 No hay elementos en la lista</p>
</template>

<style scoped>
.shopping-cart-icon {
  font-size: 2rem; /* Adjust the font-size value as per your desired size */
}
</style>