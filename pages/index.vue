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
  </main>
</template>
