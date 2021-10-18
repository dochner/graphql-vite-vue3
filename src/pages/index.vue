<script setup>
const searchOptions = reactive({
  query: '',
  limit: 10,
})

const search = (query) => {
  searchOptions.query = query
}
</script>

<template>
  <div class="container h-full relative mx-auto flex flex-col bg-gray-100">
    <div class="relative top-0 z-9998 bg-white rounded-lg shadow-lg">
      <h1
        class="
          text-4xl
          sm:text-6xl
          lg:text-7xl
          leading-none
          font-extrabold
          tracking-tight
          text-gray-900
          pt-10
          mb-8
          sm:mt-14 sm:mb-10
          max-w-6xl
          mx-auto
        "
      >
        Find
        <span
          class="
            bg-clip-text
            text-transparent
            bg-gradient-to-r
            from-green-600
            via-green-500
            to-green-400
          "
        >GitHub</span>
        Repositories:
      </h1>
      <SearchBar class="w-full" @search="search" />
    </div>
    <div
      class="
        w-full
        mx-auto
        max-w-80vw max-h-90vh
        overflow-y-auto overflow-x-hidden
        mt-48px
      "
    >
      <RepositoryList :search-options="searchOptions" />
    </div>
  </div>
</template>
