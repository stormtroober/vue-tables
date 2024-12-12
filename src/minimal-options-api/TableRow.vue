<template>
  <tr>
    <TableCell v-for="header in headers" :key="header" :value="row[header]" />
  </tr>
</template>

<script>
import TableCell from "./TableCell.vue";

export default {
  name: "TableRow",
  components: {
    TableCell
  },
  props: {
    headers: {
      type: Array,
      required: true
    },
    row: {
      type: Object,
      required: true
    }
  }
};
</script>