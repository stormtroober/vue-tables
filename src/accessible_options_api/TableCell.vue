<template>
  <td v-if="!isHeader" tabindex="0" :headers="`header-${header}`">{{ value }}</td>
  <th v-else scope="row" tabindex="0">{{ value }}</th>
</template>

<script>
export default {
  name: "TableCell",
  props: {
    value: {
      type: String,
      required: true
    },
    header: {
      type: String,
      required: true
    },
    isHeader: {
      type: Boolean,
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