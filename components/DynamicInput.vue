<script setup>
import { watch } from 'vue'

const state = defineModel('state')
const props = defineProps({
  question: {
    type: Object,
  }
});

const checkbox = reactive([]);
const checkList = reactive([]);

if (props.question.type === 'checkbox') {
  console.log(true)
  props.question.choices.map((val, i) => {
    checkbox[i] = {
      name: val,
      active: false
    }
  })
}

watch(checkbox, (newValue, oldValue) => {
  console.log(newValue, oldValue);
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
  <USelect v-else-if="question.type == 'dropdown'" :options="question.choices" />
  <div v-else-if="question.type == 'panel'">
    <img :src="question.elements[0].imageLink" class="w-96" :alt="question.elements[0].name">
    <UInput :placeholder="question.elements[1].title['es']" :icon="question.elements[1].icon"
      :type="question.elements[1].type" v-model="state" />
  </div>
  <div v-else-if="question.type == 'checkbox'">
    <UCheckbox v-for="(value, i) in question.choices" v-model="state" :label="value" />
  </div>
  <UInput v-else :placeholder="question.example['es']" :icon="question.icon" :type="question.inputType" v-model="state" />
</template>