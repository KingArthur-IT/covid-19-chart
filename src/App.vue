<template>
  <div id="app" class="container">
    <div class="row mt-5" v-if="arrNewConfirmed.length > 0">
      <div class="col">
        <h2>New Confirmed</h2>
        <line-chart :chartData="arrNewConfirmed" :option="chartOptions" label="New_Confirmed"
        :chartColors="positiveChartColors"></line-chart>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import LineChart from './components/LineChart.vue';

export default {
  name: 'App',
  components: {
    LineChart
  },
  data() {
    return {
      arrNewConfirmed: [],
      arrNewDeaths: [],
      arrNewRecovered: [],
      chartOptions: {
        responsive: true,
        maintainAspectRatio: false
      },
      positiveChartColors: {
        borderColor: "#077187",
        pointBorderColor: "#0E1428",
        pointBackgroundColor: "#AFD6AC",
        backgroundColor: "#74A57F"
      }
    };
  },
  async created() {
    const { data } = await axios.get("https://corona-api.com/timeline");
    console.log(data)
    data.data.forEach(d => {
      this.arrNewConfirmed.push({date: d.date, total: d.new_confirmed});
      this.arrNewDeaths.push({date: d.date, total: d.new_deaths});
      this.arrNewRecovered.push({date: d.date, total: d.new_recovered});
    })
    console.log(this.arrNewConfirmed)
  }
}
</script>

<style>

</style>
