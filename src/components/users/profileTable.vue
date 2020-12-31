<template>
  <v-card flat>
    <v-card-text>
      <template>
        <v-simple-table>
          <template v-slot:default>
            <tbody>
              <tr v-for="item in tableData" :key="item.name">
                <td>{{ item.name }}</td>
                <td>{{ item.value }}</td>
              </tr>
            </tbody>
          </template>
        </v-simple-table>
      </template>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: 'profileTable',
  props: {
    tableData: {
      type: Array,
    },
  },
  data() {
    return {};
  },
  methods: {},
};
</script>
