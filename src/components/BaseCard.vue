<script setup>
// Enkel prop för korttiteln
defineProps({
  title: {
    type: String,
    required: true
  }
})
</script>

<template>
  <div class="card">
    <div class="card-header">
      <h3>{{ title }}</h3>
      <!-- Named slot för actions (knappar etc) i header -->
      <div class="card-actions">
        <slot name="actions"></slot>
      </div>
    </div>
    <!-- Default slot för huvudinnehållet -->
    <div class="card-content">
      <slot></slot>
    </div>
  </div>
</template>

<style scoped>
.card {
  border: 1px solid #ccc;
  border-radius: 8px;
  margin-bottom: 1rem;
  background: white;
}

.card-header {
  padding: 1rem;
  border-bottom: 1px solid #eee;
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.card-content {
  padding: 1rem;
}

h3 {
  margin: 0;
  color: #2c3e50;
}

.card-actions {
  display: flex;
  gap: 0.5rem;
}
</style> 