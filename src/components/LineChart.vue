<template>
    <div v-if="yearData" class="line-chart">
      <canvas ref="chartCanvas"></canvas>
    </div>
  </template>
  
  <style scoped>
  .line-chart {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 400px; 
  }
  
  @media (min-width: 768px) {
    .line-chart {
      max-width: 800px; 
      margin: 0 auto; 
      height: 400px
    }
  }
  </style>
  
  <script>
  import { Chart } from 'chart.js';
  
  export default {
    props: ['yearData'],
    watch: {
      yearData: {
        immediate: true,
        handler(newData) {
          console.log('Year Data:', newData);
          if (newData) {
            this.updateChart(newData);
          }
        },
      },
    },
    methods: {
      updateChart(newData) {
        console.log('Updating Chart with:', newData);
        const ctx = this.$refs.chartCanvas?.getContext('2d');
        
        if (!ctx) {
          return;
        }
  
        if (this.chartInstance) {
          this.chartInstance.destroy();
        }
  
        const months = Object.keys(newData.avgTemperature);
        const avgTemperatures = Object.values(newData.avgTemperature);
  
        this.chartInstance = new Chart(ctx, {
          type: 'line',
          data: {
            labels: months,
            datasets: [
              {
                label: 'Average Temperature',
                data: avgTemperatures,
                borderColor: 'blue',
                fill: false,
              },
            ],
          },
          options: {
            responsive: true,
            maintainAspectRatio: false,
            scales: {
              y: {
                beginAtZero: true,
              },
            },
          },
        });
      },
    },
    beforeUnmount() {
      if (this.chartInstance) {
        this.chartInstance.destroy();
      }
    },
    data() {
      return {
        chartInstance: null,
      };
    },
  };
  </script>
  