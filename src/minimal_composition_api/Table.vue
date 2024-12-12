<template>
  <div>
    <h1>Minimal Table (Composition API)</h1>
    <!-- Loading and Error Handling -->
    <div v-if="state.loading">Loading...</div>
    <div v-else-if="state.error" class="error">{{ state.error }}</div>
    <!-- Table Rendering -->
    <table v-else border="1">
      <TableHeader :headers="state.headers" />
      <TableBody :headers="state.headers" :dataset="state.dataset" />
    </table>
  </div>
</template>

<script setup>
import { reactive, onMounted, watch } from "vue";
import Papa from "papaparse";
import TableHeader from "./TableHeader.vue";
import TableBody from "./TableBody.vue";

const state = reactive({
  headers: [],
  dataset: [],
  csvUrl: "/dataset/bank.csv",
  loading: true,
  error: null,
});

const fetchData = async () => {
  state.loading = true;
  state.error = null;
  try {
    const response = await fetch(state.csvUrl);
    const csvText = await response.text();
    Papa.parse(csvText, {
      header: true,
      complete: (results) => {
        state.headers = results.meta.fields;
        state.dataset = results.data;
      },
    });
  } catch (err) {
    state.error = "Failed to load CSV data.";
    console.error(err);
  } finally {
    state.loading = false;
  }
};

watch(() => state.csvUrl, fetchData);
onMounted(fetchData);
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
.error {
  color: red;
  font-weight: bold;
}
</style>
