<template>
  <thead>
    <tr>
      <th v-for="header in headers" :key="header">{{ header }}</th>
    </tr>
  </thead>
</template>

<script>
import { defineComponent } from "vue";

export default defineComponent({
  name: "TableHeader",
  props: {
    headers: {
      type: Array,
      required: true
    }
  }
});
</script>