<script>
import { useQuery } from "@vue/apollo-composable";
import gql from "graphql-tag";
import { computed } from "vue";

export default {
  setup() {
    const { result } = useQuery(gql`
      query data {
        getUsers {
          id
          first_name
          last_name
          address
        }
      }
    `);

    const users = computed(() => result.value?.getUsers || []);

    return {
      users,
    };
  },
};
</script>

<!-- <template>
  <div>
    <ul>
      <li v-for="user in users" :key="user.id">
        {{ user.first_name }} {{ user.last_name }} - {{ user.address }}
      </li>
    </ul>
  </div>
</template> -->
<template>
  <v-table theme="dark">
    <thead>
      <tr>
        <th class="text-left">
          ID
        </th>
        <th class="text-left">
          First Name
        </th>
        <th class="text-left">
          Last name
        </th>
        <th class="text-left">
          Address
        </th>
      </tr>
    </thead>
    <tbody>
      <tr
        v-for="user in users"
        :key="user.id"
      >
      <td>{{ user.id }}</td>
        <td>{{ user.first_name }}</td>
        <td>{{ user.last_name }}</td>
        <td>{{ user.address }}</td>
      </tr>
    </tbody>
  </v-table>
</template>