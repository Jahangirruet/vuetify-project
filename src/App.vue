<template>
  <v-responsive class="border rounded">
    <v-app>
      <v-main>
        <v-navigation-drawer>
          <v-list>
            <v-list-item title="Navigation drawer">
              <p><a href="/servers">servers</a></p>
              <p><a href="/clients">clients</a></p>
              <p><a href="/ip">iplist</a></p>
            </v-list-item>
          </v-list>
        </v-navigation-drawer>
        <v-app-bar title="VPS docs"></v-app-bar>

        <v-card class="mx-auto" prepend-icon="$vuetify">
          <router-view
        /></v-card>
      </v-main>
    </v-app>
  </v-responsive>
</template>

<script setup>
import {
  ApolloClient,
  createHttpLink,
  InMemoryCache,
} from "@apollo/client/core";

// HTTP connection to the API
const httpLink = createHttpLink({
  // You should use an absolute URL here
  uri: "http://localhost:4000/graphql",
});

// Cache implementation
const cache = new InMemoryCache();

// Create the apollo client
const apolloClient = new ApolloClient({
  link: httpLink,
  cache,
});

import { createApolloProvider } from "@vue/apollo-option";

const apolloProvider = createApolloProvider({
  defaultClient: apolloClient,
});
</script>
