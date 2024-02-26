<script setup>
const state = defineModel('state')
const props = defineProps({
  question: {
    type: Object,
  }
});

const useChoices = (choices) => {
  return choices.map((opt) => opt.text['es']);
};

// Problema de Nuxt UI para leer el nombre de los iconos
const icons = [
  'i-heroicons-user',
  'i-heroicons-user-group',
  'i-heroicons-envelope',
  'i-heroicons-phone',
  'i-heroicons-calendar',
  'i-heroicons-globe-alt',
  'i-heroicons-identification'
]
</script>

<template>
  <UInputMenu v-if="question.type == 'radiogroup'" v-model="state" :options="useChoices(question.choices)"
    :icon="question.icon" />
  <USelect v-else-if="question.type == 'dropdown'" :icon="question.icon" :options="question.choices"
    :placeholder="question.example['es']" />
  <div v-else-if="question.type == 'panel'">
    <img :src="question.elements[0].imageLink" class="w-96" :alt="question.elements[0].name">
    <UInput :placeholder="question.elements[1].title['es']" :icon="question.elements[1].icon"
      :type="question.elements[1].type" v-model="state" />
  </div>
  <UInput v-else="question.type != 'radiogroup'" :placeholder="question.example['es']" :icon="question.icon"
    :type="question.inputType" v-model="state" />
</template>