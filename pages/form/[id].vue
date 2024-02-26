<script setup>
import { onMounted, watch } from 'vue'
import survey from '../../assets/survey-structure.json'

const route = useRoute();
const router = useRouter();
const pageNavbar = ref();
const actualPage = survey.pages;
const page = ref(Number(route.query.page) - 1);

onMounted(() => {
  console.log(pageNavbar.value)
  const scroll = (route.query.page <= survey.pages.length) ? pageNavbar.value.scrollLeftMax / survey.pages.length * route.query.page : 0;
  // pageNavbar.value.scrollLeft = scroll;
  pageNavbar.value.scroll({
    left: scroll,
    behavior: "smooth"
  })
});

async function onSubmit(event) {
  console.log(state);


  if ((page.value + 1) < survey.pages.length) {
    page.value++
    router.push(`?page=${page.value + 1}`);
  }
}

const state = reactive({});

watch(page, async (newQuestion, oldQuestion) => {
  console.log('Quest', newQuestion)

  actualPage[page.value].elements.forEach((el) => {
    state[el.name] = undefined;
  });
});
</script>

<template>
  {{ $route.query.page }}
  <div ref="pageNavbar" class="overflow-x-auto">
    <ul class="flex flex-row justify-center gap-4 min-w-[900px] my-8 ">
      <li v-for="i in survey.pages.length"
        class="inline-block w-8 h-8 rounded bg-[#5e1780] text-center align-middle leading-8"
        :class="{ 'bg-[#d13ce3] font-bold': i == $route.query.page }">{{ i
        }}
      </li>
    </ul>
  </div>
  <h1>{{ actualPage[page].title.es }}</h1>

  <UForm :state="state" class="space-y-4" @submit="onSubmit">

    <UFormGroup v-for="question in actualPage[page].elements" :label="question.title['es']"
      :required="question.isRequired">
      <dynamic-input :question="question" v-model:state="state[question.name]" />
    </UFormGroup>
    <UButton type="submit">
      Siguiente sección
    </UButton>
  </UForm>
</template>