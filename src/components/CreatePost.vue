<script setup>
import BaseButton from './BaseButton.vue'

// Props som tas emot från App.vue
const props = defineProps({
  title: String,
  body: String,
  isBold: Boolean
})

// Definierar vilka custom events som komponenten kan emittera
const emit = defineEmits(['titleChanged', 'bodyChanged', 'update:isBold'])

// Funktion som växlar bold-status och emitterar förändringen
const toggleBold = () => {
  emit('update:isBold', !props.isBold)
}
</script>

<template>
  <div class="create-post">
    <div class="title-container">
      <!-- Input som använder one-way binding (:value) och emitterar ändringar -->
      <input 
        type="text" 
        :value="title"
        @input="emit('titleChanged', $event.target.value)"
        placeholder="Skriv din titel här..."
        class="title-input"
        :class="{ 'bold': isBold }"
      >
      <!-- Återanvändbar knappkomponent för bold-funktionen -->
      <BaseButton 
        @click="toggleBold"
        :active="isBold"
      >
        B
      </BaseButton>
    </div>
    
    <!-- Textarea fungerar på samma sätt som input ovan -->
    <textarea 
      :value="body"
      @input="emit('bodyChanged', $event.target.value)"
      placeholder="Skriv ditt inlägg här..."
      class="body-input"
    ></textarea>
  </div>
</template>

<style scoped>
.create-post {
  margin: 1rem 0;
  display: flex;
  flex-direction: column;
  gap: 1rem;
}

.title-container {
  display: flex;
  gap: 0.5rem;
}

.title-input {
  flex: 1;
}

.title-input, .body-input {
  width: 100%;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.body-input {
  min-height: 150px;
  resize: vertical;
}

.bold-btn {
  padding: 0.5rem 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  background: white;
  cursor: pointer;
  font-weight: bold;
}

.bold-btn.active {
  background: #e0e0e0;
}

.title-input.bold {
  font-weight: bold;
}
</style> 