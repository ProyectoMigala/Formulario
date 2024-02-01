<script setup>
import { useProductsStore } from "../assets/stores/MisCompras.js";

const productList = useProductsStore();

useHead({
  charset: "utf-8",
  viewport: "width=device-width, initial-scale=1",
  title: "Registro Proyecto Migala",
  meta: [
    {
      name: "Registro Proyecto Migala",
      content: "Formulario de resgistro al patrón de miembros del proyecto Migala.",
    },
  ],
  link: [
    {
      rel: "apple-touch-icon",
      sizes: "180x180",
      href: "/favicon/apple-touch-icon.png",
    },
    {
      rel: "icon",
      type: "image/png",
      sizes: "32x32",
      href: "/favicon/favicon-32x32.png",
    },
    {
      rel: "icon",
      type: "image/png",
      sizes: "16x16",
      href: "/favicon/favicon-16x16.png",
    },
    {
      rel: "manifest",
      href: "/site.webmanifest",
    },
  ],
  // script: [
  //   {
  //     src: "/sw.js",
  //   },
  // ],
});

const people = ['Mexicana', 'Extranjera naturalizada', 'Extranjera']

const selected = ref(people[0])

const columns = reactive([
  {
    key: "name",
    label: "Articulo",
  },
  { key: "category", label: "Categoria" },
  { key: "price", label: "Precio" },
  { key: "quantity", label: "Cantidad" },
  { key: "unit", label: "Unidad" },
  { key: "total", label: "Total" },
  { key: "actions" },
]);

const isOpen = ref(false);

let id = null;

function upData() {
  const d = new Date().toLocaleString("es-MX").split(", ");
  fetch(`https://${process.env.DOMAIN}/.netlify/functions/<function-name>`, {
    method: "PUT",

    headers: {
      "Content-Type": "application/json",
    },
    body: null,
  })
    .then((response) => response.blob())
    .catch((error) => console.error("Error:", error))
    .then((blob) => {
      console.log("Success:", blob);
    });
}

</script>

<template>
  <main class="container mx-auto">
    <UFormGroup label="¿Cómo te gustaría que nos refiramos a ti?" required>
      <UInput placeholder="Rick, Dai, Pepe, etc..." icon="i-heroicons-envelope" />
    </UFormGroup>
    <UFormGroup label="Correo electrónico" required>
      <UInput placeholder="tucorreo@email.com" icon="i-heroicons-envelope" />
    </UFormGroup>
    <UFormGroup label="Teléfono celular" required>
      <UInput placeholder="5516432324" icon="i-heroicons-envelope" />
    </UFormGroup>
    <UFormGroup label="Fecha de nacimiento" required>
      <UInput icon="i-heroicons-envelope" type="date" value="2000-01-01" />
    </UFormGroup>
    <UFormGroup label="¿Cuál es tu nacionalidad?" required>
      <UInputMenu v-model="selected" :options="people" icon="i-heroicons-envelope" />
    </UFormGroup>
  </main>
</template>
