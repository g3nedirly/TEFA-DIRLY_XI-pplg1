<template>
  <div>
      <canvas id="myChart"></canvas>
  </div>
</template>

<script setup>
import Chart from 'chart.js/auto';

const labels=[
  'january',
  'february',
  'march',
  'april',
  'may',
  'june',
  
];

const data= {
  labels : labels,
  datasets: [{
      label: 'Pengunjung',
      backgroundColor: [
      'rgb(217, 217, 217)',  
      'rgb(217, 217, 217)',
      'rgb(217, 217, 217)',
      'rgb(217, 217, 217)',
      'rgb(217, 217, 217)',
      'rgb(158, 90, 94)',
      ],
      borderColor: 'rgb(255, 99, 132)',
      data: [5, 15, 12, 12, 20],
  }]
};

const config = {
  type: 'bar',
  data: data,
  options: {}
};

onMounted(()=>{
  const myChart = new Chart(
  document.getElementById('myChart'),
  config
);
})
</script>