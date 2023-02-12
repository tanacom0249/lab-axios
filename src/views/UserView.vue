<template>
  <div>
    <h1 style="text-align: center">
      <h1>พยากรณ์อากาศ</h1>
    </h1>
    <h2 style="text-align: center">
      <h2>แสดงข้อมูลพยากรณ์อากาศ</h2>
    </h2>
    <button @click="loadUser()" class="button">Load Forecast Data</button>
    <div style="text-align: center; font-size: 30px">
      {{ ForecastProduct }} {{ ForecastInit }}
  </div>
<!--{{ ForecastData }}-->
<table style="width:75%">
  <thead>
    <tr>
      <th rowspan="2" style="font-weight: bold">Timepoint</th>
      <th rowspan="2" style="font-weight: bold">Cloudcover</th>
      <th rowspan="2" style="font-weight: bold">Seeing</th>
      <th rowspan="2" style="font-weight: bold">Transparency</th>
      <th rowspan="2" style="font-weight: bold">Lifted index</th>
      <th rowspan="2" style="font-weight: bold">
        Relative average<br />humidity at 2 meters
      </th>
      <th colspan="2" style="font-weight: bold">Wind velocity at 10 meters</th>
      <th rowspan="2" style="font-weight: bold">Temperature <br />at 2 meters</th>
      <th rowspan="2" style="font-weight: bold">PrecType</th>
    </tr>
    <tr>  
      <th style="font-weight: bold">Direction</th>
      <th style="font-weight: bold">Speed</th>
    </tr>
  </thead>
  <tbody v-for="forecast in ForecastData" :key="forecast.id">
    <tr>
      <td>{{ forecast.timepoint }}</td>
      <td>{{ forecast.cloudcover }}</td>
      <td>{{ forecast.seeing }}</td>
      <td>{{ forecast.transparency }}</td>
      <td>{{ forecast.lifted_index }}</td>
      <td>{{ forecast.rh2m }}</td>
      <td>{{ forecast.wind10m.direction }}</td>
      <td>{{ forecast.wind10m.speed }}</td>
      <td>{{ forecast.temp2m }}</td>
      <td>{{ forecast.prec_type }}</td>
    </tr>
  </tbody>
</table>
</div>
</template>

<script setup>
import axios from "axios";
import { ref } from "vue";

const ForecastProduct = ref();
const ForecastInit = ref();
const ForecastData = ref([]);
const url = ref(
  "https://www.7timer.info/bin/astro.php?lon=113.2&lat=23.1&ac=0&unit=metric&output=json&tzshift=0"
);

function loadUser() {
  axios
    .get(url.value)
    .then((response) => {
      ForecastProduct.value = response.data.product;
      ForecastInit.value = response.data.init;
      ForecastData.value = response.data.dataseries;
    })
    .catch((err) => {
      console.log(err);
    });
  }
</script>

<style>
table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
  text-align: center;
  margin-inline: auto;
}
table {
  margin-block-end: 20px;
}
thead {
  background-color: aqua;
}
button{
  display: block;
  margin-inline: auto;
  margin-block: 25px;
  font-size: 30px;
}
</style>
