<script setup>
// Prop för att hantera knappens aktiva tillstånd
defineProps({
  active: {
    type: Boolean,
    default: false
  }
})
</script>

<template>
  <!-- Återanvändbar knapp med conditional styling baserat på active-prop -->
  <button 
    class="base-button"
    :class="{ 'active': active }"
  >
    <!-- Slot gör knappen flexibel - kan innehålla text eller ikon -->
    <slot></slot>
  </button>
</template>

<style scoped>
.base-button {
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  background: white;
  cursor: pointer;
}

.base-button.active {
  background: #e0e0e0;
}
</style> 