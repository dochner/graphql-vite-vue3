<script setup>
import { ApolloClients } from '@vue/apollo-composable'
import {
  ApolloClient,
  ApolloLink,
  InMemoryCache,
  from,
  HttpLink,
} from '@apollo/client/core'

const token = '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'

const additiveLink = from([
  new ApolloLink((operation, forward) => {
    operation.setContext(({ headers }) => ({
      headers: {
        ...headers,
        authorization: token ? `Bearer ${token}` : null,
      },
    }))
    return forward(operation) // Go to the next link in the chain. Similar to `next` in Express.js middleware.
  }),
  new HttpLink({ uri: 'https://api.github.com/graphql' }),
])

const apolloClient = new ApolloClient({
  link: additiveLink,
  cache: new InMemoryCache(),
})
// https://github.com/vueuse/head
// you can use this to manipulate the document head in any components,
// they will be rendered correctly in the html results with vite-ssg
useHead({
  title: 'Github Repos',
  meta: [{ name: 'description', content: 'Opinionated Vite Starter Template' }],
})

provide(ApolloClients, {
  default: apolloClient,
})
</script>

<template>
  <router-view />
</template>
