<script setup>
// Props definierar vilken data komponenten kan ta emot från sin parent
defineProps({
  title: {
    type: String,
    required: true  // Detta prop måste skickas med
  },
  body: {
    type: String,
    required: true
  },
  isBold: {
    type: Boolean,
    default: false  // Om inget värde skickas med används detta som standard
  }
})
</script>

<template>
  <div class="preview-post">
    <!-- Använder conditional class binding för att styra bold-formatering -->
    <h2>Titel: <span :class="{ 'bold': isBold }">{{ title }}</span></h2>
    <div class="post-body">
      <p>Innehåll: {{ body }}</p>
    </div>
  </div>
</template>

<style scoped>
.preview-post {
  padding: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin: 1rem 0;
}

h2 {
  margin-top: 0;
  color: #2c3e50;
  margin-bottom: 1rem;
  font-weight: 200;
}

.post-body {
  line-height: 1.6;
}

.bold {
  font-weight: 800;
}
</style> 