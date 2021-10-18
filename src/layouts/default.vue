<template>
  <main class="h-screen box-border flex flex-col justify-center">
    <router-view />
  </main>
</template>

<style lang="postcss">
* {
  scrollbar-color: rgb(39, 255, 143) rgba(179, 192, 201, 1);
  scrollbar-width: thin;
}

::-webkit-scrollbar {
  @apply w-10px;

  &-track {
    @apply bg-gray-300 rounded-10px;
  }

  &-thumb {
    @apply bg-green-600 rounded-full hover:bg-green-400 transition-colors duration-300;
  }
}
</style>
