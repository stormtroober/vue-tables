<template>
  <tr>
    <TableCell v-for="header in headers" :key="header" :value="row[header]" />
  </tr>
</template>

<script>
import { defineComponent } from "vue";
import TableCell from "./TableCell.vue";

export default defineComponent({
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
});
</script>