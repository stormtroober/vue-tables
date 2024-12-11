<template>
    <div>
      <h1 id="tableTitle">Bank Dataset</h1>
      <div role="region" aria-labelledby="tableTitle" tabindex="0">
        <table border="1" aria-describedby="tableDesc">
          <caption id="tableDesc">Bank customer information and transactions</caption>
          <TableHeader :headers="headers" />
          <TableBody :dataset="dataset" :headers="headers" />
        </table>
      </div>
    </div>
  </template>
  
  <script>
  import { ref, onMounted } from "vue";
  import Papa from "papaparse";
  import TableHeader from "./TableHeader.vue";
  import TableBody from "./TableBody.vue";
  
  export default {
    name: "AccessibleTable",
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
    margin-bottom: 1em;
  }
  th, td {
    padding: 10px;
    border: 1px solid #ccc;
    text-align: left;
  }
  th {
    background-color: #f9f9f9;
  }
  [role="region"] {
    max-height: 600px;
    overflow: auto;
  }
  </style>
  