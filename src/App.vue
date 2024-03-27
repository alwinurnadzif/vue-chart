<template>
  <div class="container">
    <div class="row">
      <div class="col-12 mt-5">
        <div class="card shadow">
          <div class="card-body">
            <h1>Hello</h1>
            <div class="row">
              <div class="col-12 col-md-4 mb-3">
                <DoughnutChart
                  :chartData="testData"
                  :options="options"
                ></DoughnutChart>
              </div>
              <div class="col-12 col-md-4 mb-3">
                <LineChart :chartData="testData" :options="options"></LineChart>
              </div>
              <div class="col-12 col-md-4 mb-3">
                <BarChart :chartData="testData" :options="options"></BarChart>
              </div>
            </div>
            <button @click="updateData">update chart</button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { DoughnutChart, LineChart, BarChart } from "vue-chart-3";
import { Chart, registerables } from "chart.js";
import { computed, ref } from "vue";

Chart.register(...registerables);

const data = ref([20, 40, 60, 70, 5]);

const options = ref({
  responsive: true,
  animations: {
    tension: {
      duration: 1000,
      easing: "linear",
      from: 1,
      to: 0,
      loop: true,
    },
  },
  plugins: {
    legend: {
      display: false,
    },
  },
  scales: {
    x: {
      grid: {
        display: false,
      },
    },
  },
});

const testData = computed(() => ({
  labels: ["Paris", "Nîmes", "Toulon", "Perpignan", "Autre"],
  datasets: [
    {
      data: data.value,
      backgroundColor: ["#77CEFF", "#0079AF", "#123E6B", "#97B0C4", "#A5C8ED"],
    },
  ],
}));

const randomNumber = () => Math.floor(Math.random() * 10) + 1;

const updateData = () => {
  data.value = [
    randomNumber(),
    randomNumber(),
    randomNumber(),
    randomNumber(),
    randomNumber(),
  ];
};
</script>
