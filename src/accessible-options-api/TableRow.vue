<template>
  <tr>
    <TableCell v-for="(header, index) in headers" :key="index" :header="header" :value="row[header]" :isHeader="index === 0" />
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