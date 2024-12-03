<script setup>
import { ref } from 'vue'
import CreatePost from './components/CreatePost.vue'
import PreviewPost from './components/PreviewPost.vue'
import BaseCard from './components/BaseCard.vue'
import BaseButton from './components/BaseButton.vue'

const post = ref({
  title: '',
  body: ''
})

const isBold = ref(false)

// METOD 1: Separata funktioner i script-delen
// Fördelar:
// - Tydligt namngivna funktioner
// - Lätt att lägga till mer logik senare
// - Funktionerna kan återanvändas
// - Följer "separation of concerns" - logik i script, template i template
const handleTitleChange = (newTitle) => post.title = newTitle
const handleBodyChange = (newBody) => post.body = newBody
const handleBoldToggle = (value) => isBold = value
</script>

<template>
  <div class="app">
    <h1>Inlägg Förhandsgranskare</h1>
    
    <BaseCard title="Förhandsgranskning">
      <template #actions>
        <BaseButton>
          <i class="fas fa-expand"></i>
        </BaseButton>
      </template>
      <PreviewPost 
        :title="post.title" 
        :body="post.body"
        :isBold="isBold"
      />
    </BaseCard>

    <BaseCard title="Skapa inlägg">
      <template #actions>
      </template>

      {/* METOD 1: Använder separata funktioner */}
      {/* Fördelar: */}
      {/* - Renare template-kod */}
      {/* - Lättare att underhålla */}
      {/* - Bättre för större applikationer */}
      <CreatePost 
        :title="post.title"
        :body="post.body"
        :isBold="isBold"
        @titleChanged="handleTitleChange"
        @bodyChanged="handleBodyChange"
        @update:isBold="handleBoldToggle"
      />

      {/* METOD 2: Använder inline arrow functions */}
      {/* Fördelar: */}
      {/* - All logik är synlig direkt i template */}
      {/* - Bra för enkel logik */}
      {/* - Färre filer att hoppa mellan */}
      <!-- <CreatePost 
        :title="post.title"
        :body="post.body"
        :isBold="isBold"
        @titleChanged="(newTitle) => post.title = newTitle"
        @bodyChanged="(newBody) => post.body = newBody"
        @update:isBold="(value) => isBold = value"
      /> -->

      {/* Exempel på när Metod 1 är bättre - om vi behöver lägga till validering: */}
      {/* 
      const handleTitleChange = (newTitle) => {
        if (newTitle.length > 100) {
          alert('Titel för lång!')
          return
        }
        post.title = newTitle
      }
      */}

      {/* Samma sak med Metod 2 blir klumpigt: */}
      {/* 
      @titleChanged="(newTitle) => {
        if (newTitle.length > 100) {
          alert('Titel för lång!')
          return
        }
        post.title = newTitle
      }"
      */}
    </BaseCard>
  </div>
</template>

<style scoped>
.app {
  max-width: 800px;
  margin: 0 auto;
  padding: 1rem;
}

h1 {
  color: #2c3e50;
  margin-bottom: 2rem;
}
</style>
