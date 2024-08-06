<script>
import { useQuery } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { computed } from "vue";

export default {
  setup() {
    const { result } = useQuery(gql`
      query data {
        getClients {
          core
          disk
          email
          expiryday
          id
          ipaddress
          ippassword
          ram
          username
        }
      }
    `);

    const clients = computed(() => result.value?.getClients || []);

    return {
      clients,
    };
  },
};
</script>

<template>
  <div>
    <v-table theme="dark">
      <thead>
        <tr>
          <th class="text-left">ID</th>
          <th class="text-left">IP Address</th>
          <th class="text-left">Username</th>
          <th class="text-left">Password</th>
          <th class="text-left">Email</th>
          <th class="text-left">RAM</th>
          <th class="text-left">Core</th>
          <th class="text-left">Disk</th>
          <th class="text-left">Expiry Date</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="client in clients" :key="client.id">
          <td>{{ client.id }}</td>
          <td>{{ client.ipaddress }}</td>
          <td>{{ client.username }}</td>
          <td>{{ client.ippassword }}</td>
          <td>{{ client.email }}</td>
          <td>{{ client.ram }}</td>
          <td>{{ client.core }}</td>
          <td>{{ client.disk }}</td>
          <td>{{ client.expiryday }}</td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>
