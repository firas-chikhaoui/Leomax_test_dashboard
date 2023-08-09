<template>
  <table class="data-table">
    <thead>
      <tr>
        <th>Year</th>
        <th>Avg Year Temp</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="year in years" :key="year.id" @click="selectYear(year)">
        <td>{{ year.year }}</td>
        <td>{{ year.avgYearTemp }}</td>
      </tr>
    </tbody>
  </table>
</template>
  
<style scoped>
.data-table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 20px;
}

.data-table th,
.data-table td {
  padding: 10px;
  border: 1px solid #ccc;
  text-align: center;
}

.data-table th {
  background-color: #f0f0f0;
  font-weight: bold;
}

.data-table tr:hover {
  background-color: #f5f5f5;
  cursor: pointer;
}
</style>
  
  
<script>
export default {
  props: ['years'],
  methods: {
    selectYear(yearData) {
      console.log('Selected Year:', yearData);
      this.$emit('show-chart', yearData);
    },
  },
};
</script>
  
  