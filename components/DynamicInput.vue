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
</script>

<template>
  <UInput v-if="question.type != 'radiogroup'" :placeholder="question.example['es']" icon="i-heroicons-envelope"
    :type="question.type" v-model="state" />
  <UInputMenu v-else-if="question.type == 'radiogroup'" v-model="state" :options="useChoices(question.choices)"
    icon="i-heroicons-envelope" />
</template>