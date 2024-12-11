<template>
  <td>{{ value }}</td>
</template>

<script>
export default {
  name: "TableCell",
  props: {
    value: {
      type: String,
      required: true
    }
  }
};
</script>