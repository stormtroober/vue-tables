<template>
  <tbody>
    <tr v-for="row in dataset" :key="row.id">
      <td v-for="header in headers" :key="header">{{ row[header] }}</td>
    </tr>
  </tbody>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "TableBody",
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
});
</script>