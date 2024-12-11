<template>
  <tbody>
    <tr v-for="(row, rowIndex) in dataset" :key="rowIndex">
      <th scope="row" tabindex="0">{{ row[headers[0]] }}</th>
      <td tabindex="0"
        v-for="(header) in headers.slice(1)"
        :key="header"
        :headers="`header-${header}`"
      >
        {{ row[header] }}
      </td>
    </tr>
  </tbody>
</template>

<script>
export default {
  name: "TableBody",
  props: {
    dataset: {
      type: Array,
      required: true
    },
    headers: {
      type: Array,
      required: true
    }
  }
};
</script>

<style scoped>
td, th {
  padding: 8px;
  text-align: left;
}

tr:hover {
  background-color: #f5f5f5;
}

tr:focus-within {
  outline: 2px solid #007bff;
  outline-offset: -2px;
}

[role="cell"]:focus, [role="columnheader"]:focus {
  outline: 2px solid #007bff;
  outline-offset: -2px;
}
</style>