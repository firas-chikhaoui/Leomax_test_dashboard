<template>
  <div class="dashboard">
    <h1 class="dashboard-title">Temperature Dashboard</h1>
    <div class="dashboard-content">
      <data-table :years="years" @show-chart="showChart"></data-table>
      <line-chart :yearData="selectedYearData"></line-chart>
    </div>
  </div>
</template>

<style scoped>
.dashboard {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
}

.dashboard-title {
  font-size: 24px;
  text-align: center;
  margin-bottom: 20px;
}

.dashboard-content {
  display: flex;
  flex-direction: column;
  gap: 20px;
}
</style>


<script>
import axios from 'axios';
import DataTable from './components/DataTable.vue';
import LineChart from './components/LineChart.vue';

export default {
  components: {
    DataTable,
    LineChart,
  },
  data() {
    return {
      years: [],
      selectedYearData: null,
    };
  },
  async created() {
    try {
      const response = await axios.get('http://localhost:3000/weather');
      this.years = response.data;
      console.log('Fetched Years:', this.years);
    } catch (error) {
      console.error('Error fetching data:', error);
    }
  },
  methods: {
    showChart(yearData) {
      console.log('Selected Year Data for Chart:', yearData);
      this.selectedYearData = yearData;
    },
  },
};
</script>


