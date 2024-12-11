<template>
    <thead>
      <tr role="row">
        <th tabindex="0"
          v-for="header in headers"
          :key="header"
          :id="`header-${header}`"
          scope="col"
          role="columnheader"
        >
          {{ header }}
          <span class="sr-only">, press Enter to sort</span>
        </th>
      </tr>
    </thead>
  </template>
  
  <script>
  export default {
    name: "TableHeader",
    props: {
      headers: {
        type: Array,
        required: true,
      },
    },
  };
  </script>
  
  <style scoped>
  th {
    font-weight: bold;
    text-transform: capitalize;
    cursor: pointer;
    user-select: none;
    position: relative;
  }
  
  th:hover {
    background-color: #eee;
  }
  
  th:focus {
    outline: 2px solid #007bff;
    outline-offset: -2px;
  }
  
  /* Screen reader only text */
  .sr-only {
    position: absolute;
    width: 1px;
    height: 1px;
    padding: 0;
    margin: -1px;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    white-space: nowrap;
    border: 0;
  }
  </style>