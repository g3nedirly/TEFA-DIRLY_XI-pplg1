<template>
  <div>
    <canvas id="myChart"></canvas>
  </div>
</template>


<script setup>
import Chart from 'chart.js/auto';

const labels = [
  'Januari',
  'Februari',
  'March',
  'April',
  'May',
  'June',
];

  const data = {
    labels: labels,
    datasets: [{
      label: 'My First dataset',
      backgroundColor: 'rgb(211, 211, 211)',
      borderColor: 'rgb(255, 99, 132)',
      data: [13, 19, 22, 17, 18, 20, 30, 35],
    }]
  };

  const config = {
    type: 'bar',
    data: data,
    Options: {}
  };

onMounted(() => {
  const myChart = new Chart (
    document.getElementById('myChart'),
    config
  );
})
</script>

<template>
  <div>
    <canvas id="myChart"></canvas>
  </div>
</template>