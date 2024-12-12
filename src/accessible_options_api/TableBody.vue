<template>
  <tbody>
    <TableRow v-for="(row, rowIndex) in dataset" :key="rowIndex" :row="row" :headers="headers" />
  </tbody>
</template>

<script>
import TableRow from "./TableRow.vue";

export default {
  name: "TableBody",
  components: {
    TableRow
  },
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