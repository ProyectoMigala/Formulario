<script setup>
import { marked } from "marked";
import pres from "../md/presentacion.md?raw";

const presentation = marked.parse(pres);

console.log(presentation)

</script>

<template>
  <div class="render" v-html="presentation">
  </div>
</template>

<style>
.render {
  font-size: 16px;
}

.render h1 {
  font-weight: 700;
  font-size: 24px;
}
</style>