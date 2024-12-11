<template>
  <tbody>
    <TableRow v-for="row in dataset" :key="row.id" :row="row" :headers="headers" />
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
    headers: {
      type: Array,
      required: true
    },
    dataset: {
      type: Array,
      required: true
    }
  }
};
</script>