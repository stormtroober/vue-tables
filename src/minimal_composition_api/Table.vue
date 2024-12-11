<template>
  <div>
    <h1>Minimal Table (Composition API)</h1>
    <table border="1">
      <TableHeader :headers="headers" />
      <TableBody :headers="headers" :dataset="dataset" />
    </table>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";
import Papa from "papaparse";
import TableHeader from "./TableHeader.vue";
import TableBody from "./TableBody.vue";

export default {
  name: "TableComposition",
  components: {
    TableHeader,
    TableBody
  },
  setup() {
    const headers = ref([]);
    const dataset = ref([]);

    onMounted(() => {
      fetch("/dataset/bank.csv")
        .then((response) => response.text())
        .then((csvText) => {
          Papa.parse(csvText, {
            header: true,
            complete: (results) => {
              headers.value = results.meta.fields;
              dataset.value = results.data;
            }
          });
        });
    });

    return {
      headers,
      dataset
    };
  }
};
</script>

<style scoped>
table {
  width: 100%;
  border-collapse: collapse;
}
th, td {
  padding: 8px;
  text-align: left;
}
th {
  background-color: #f4f4f4;
}
</style>