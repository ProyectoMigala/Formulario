<script setup>
import { onMounted, computed } from 'vue'
import survey from '../../assets/survey-structure.json'

const route = useRoute();
const pageNavbar = ref();

onMounted(() => {
  console.log(pageNavbar.value)
  const scroll = (route.query.page <= survey.pages.length) ? pageNavbar.value.scrollLeftMax / survey.pages.length * route.query.page : 0;
  // pageNavbar.value.scrollLeft = scroll;
  pageNavbar.value.scroll({
    left: scroll,
    behavior: "smooth"
  })
});

const useChoices = (choices) => {
  return choices.map((opt) => opt.text['es']);
};

async function onSubmit(event) {
  // Do something with data
  console.log(event.data)
}

const state = reactive({});
survey.pages[2].elements.forEach((el) => {
  state[el.name] = undefined;
})
</script>

<template>
  <div ref="pageNavbar" class="overflow-x-auto">
    <ul class="flex flex-row justify-center gap-4 min-w-[900px] my-8 ">
      <li v-for="i in survey.pages.length"
        class="inline-block w-8 h-8 rounded bg-[#5e1780] text-center align-middle leading-8"
        :class="{ 'bg-[#d13ce3] font-bold': i == $route.query.page }">{{ i
        }}
      </li>
    </ul>
  </div>
  <h1>{{ survey.pages[2].title.es }}</h1>

  <UForm :state="state" class="space-y-4" @submit="onSubmit">
    <UFormGroup v-for="question in survey.pages[2].elements" :label="question.title['es']"
      :required="question.isRequired">
      <UInput v-if="question.type != 'radiogroup'" :placeholder="question.example['es']" icon="i-heroicons-envelope"
        :type="question.type" v-model="state[question.name]" />
      <UInputMenu v-else-if="question.type == 'radiogroup'" v-model="state[question.name]"
        :options="useChoices(question.choices)" icon="i-heroicons-envelope" />
    </UFormGroup>
    <UButton type="submit">
      Submit
    </UButton>
  </UForm>
</template>