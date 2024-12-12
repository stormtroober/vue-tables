<template>
  <td>{{ value }}</td>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "TableCell",
  props: {
    value: {
      type: String,
      required: true
    }
  }
});
</script>