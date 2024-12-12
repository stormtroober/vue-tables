<template>
  <div>
    <h1>Minimal Table (Options API)</h1>
    <table border="1">
      <TableHeader :headers="headers" />
      <TableBody :headers="headers" :dataset="dataset" />
    </table>
  </div>
</template>

<script>
import Papa from "papaparse";
import TableHeader from "./TableHeader.vue";
import TableBody from "./TableBody.vue";

export default {
  name: "Table",
  components: {
    TableHeader,
    TableBody
  },
  data() {
    return {
      headers: [],
      dataset: []
    };
  },
  mounted() {
    fetch("/dataset/bank.csv")
      .then((response) => response.text())
      .then((csvText) => {
        Papa.parse(csvText, {
          header: true,
          complete: (results) => {
            this.dataset = results.data;
            this.headers = results.meta.fields;
          },
          error: (error) => {
            console.error("Error parsing CSV:", error);
          }
        });
      })
      .catch((error) => {
        console.error("Error fetching CSV:", error);
      });
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