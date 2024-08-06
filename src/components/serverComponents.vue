<script>
import { useQuery } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { computed } from "vue";

export default {
  setup() {
    const { result } = useQuery(gql`
      query data {
        gerServers {
          serverIP
          sdisk
          score
          sram
        }
      }
    `);

    const servers = computed(() => result.value?.gerServers || []);

    return {
      servers,
    };
  },
};
</script>

<template>
  <div>
    <v-table theme="dark">
      <thead>
        <tr>
          <th class="text-left">Server IP</th>
          <th class="text-left">RAM</th>
          <th class="text-left">Core</th>
          <th class="text-left">Disk</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="server in servers" :key="server.id">
          <td>{{ server.serverIP }}</td>
          <td>{{ server.sram }}</td>
          <td>{{ server.score }}</td>
          <td>{{ server.sdisk }}</td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>
