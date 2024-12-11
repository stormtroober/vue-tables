<template>
    <div>
      <h1>Minimal Table (Composition API)</h1>
      <table border="1">
        <thead>
          <tr>
            <th v-for="header in headers" :key="header">{{ header }}</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="row in dataset" :key="row.id">
            <td v-for="header in headers" :key="header">{{ row[header] }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from "vue";
  import Papa from "papaparse";
  
  export default {
    name: "TableComposition",
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
                dataset.value = results.data;
                headers.value = results.meta.fields;
              },
              error: (error) => {
                console.error("Error parsing CSV:", error);
              }
            });
          })
          .catch((error) => {
            console.error("Error fetching CSV:", error);
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