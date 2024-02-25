<script setup>

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
  script: [
    {
      src: "/sw.js",
    },
  ],
});
</script>

<template>
  <header class="relative w-full min-h-40 overflow-hidden bg-[#5e1780] py-8">
    <div class=" flex flex-col justify-around items-center">
      <img class="w-1/6 pt-4 object-contain animate-spin-slow" src="/image/logo_pm_white.png" alt="">
      <h4 class="pt-4 text-lg font-bold">PROYECTO MIGALA</h4>
    </div>
    <div class="absolute w-full h-full">
      <div class="absolute -top-96 -left-64 w-[510px] h-[510px] bg-[#d13ce3] rounded-full opacity-30 z-10"></div>
      <div class="absolute -top-72 -right-80 w-[410px] h-[410px] bg-[#a2be1d] rounded-full opacity-30 z-10"></div>
    </div>
  </header>
  <main class="container mx-auto">
    <div>
      <div class=" pt-20 pb-4">
        <h3 class="text-[#5e1780] dark:text-[#d13ce3] text-3xl font-bold">Registro de participación</h3>
      </div>
    </div>
    <slot />
  </main>
</template>

<style>
.animate-spin-slow {
  animation: spin 7s linear infinite;
}

@keyframes spin {
  from {
    transform: rotate(0deg);
  }

  to {
    transform: rotate(360deg);
  }
}
</style>