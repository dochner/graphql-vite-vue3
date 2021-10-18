<script setup>
import { defineComponent, toRefs } from 'vue'
import { useQuery, useResult } from '@vue/apollo-composable'
import { SearchResultItemConnection } from '@octokit/graphql-schema'
import { SEARCH_REPOS } from '~/graphql/documents.js'

const props = defineProps({
  searchOptions: {
    type: Object,
    default() {
      return { query: '', limit: 10 }
    },
  },
})

const { searchOptions } = toRefs(props)

const { result, loading, error } = useQuery(SEARCH_REPOS, searchOptions)

const repositories = useResult(
  result,
  [],
  data => data.search && data.search.edges,
)
</script>

<template>
  <div v-if="loading" class="flex justify-center">
    <p class="text-xl font-bold text-gray-500">
      Request is loading...
    </p>
  </div>
  <div v-else-if="error" class="flex justify-center">
    <p class="text-xl font-bold text-red-600">
      Request has failed!
    </p>
  </div>
  <div v-else-if="repositories.length">
    <ul class="md:block max-w-6xl mx-auto">
      <li
        v-for="repository in repositories"
        :key="repository.node.id"
        class="relative mb-8"
      >
        <!-- <div>{{ repository.topic.name }}</div> -->
        <Repository :repository="repository" :search-options="searchOptions" />
      </li>
    </ul>
  </div>
</template>
