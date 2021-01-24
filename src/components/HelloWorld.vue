<template>
  <div class="hello">
    <div>
      <img v-on:click="updateChart(0)" card src="../assets/0.svg"/>
      <img v-on:click="updateChart(1)" src="../assets/05.svg"/>
      <img v-on:click="updateChart(2)" src="../assets/1.svg"/>
      <img v-on:click="updateChart(3)" src="../assets/2.svg"/>
      <img v-on:click="updateChart(4)" src="../assets/3.svg"/>
      <img v-on:click="updateChart(5)" src="../assets/5.svg"/>
      <img v-on:click="updateChart(6)" src="../assets/8.svg"/>
      <img v-on:click="updateChart(7)" src="../assets/13.svg"/>
      <img v-on:click="updateChart(8)" src="../assets/20.svg"/>
      <img v-on:click="updateChart(9)" src="../assets/40.svg"/>
      <img v-on:click="updateChart(10)" src="../assets/100.svg"/>
      <img src="../assets/unclear.svg"/>
      <img src="../assets/break.svg"/>
      <img src="../assets/afk.svg"/>
      <div id="chart">
        <apexchart type="bar" height="350" :options="chartOptions" :series="series"></apexchart>
        <apexchart type="bar" height="100" :options="chartOptions2" :series="series2"></apexchart>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'HelloWorld',
  props: {
    msg: String,
  },
  data: function () {
    return {
      series: [{ data: [0,0,0,0,0,0,0,0,0,0,0]}],
      chartOptions: {
        chart: {
          height: 350,
          type: 'bar',
          // events: {
          //   click: function(chart, w, e) {
          //     // console.log(chart, w, e)
          //   }
          // }
        },
        plotOptions: {
          bar: {
            columnWidth: '45%',
            distributed: true
          }
        },
        colors: ["#9E9E9E", "#8BC34A", "#4CAF50", "#009688", "#00BCD4", "#03A9F4", "#2196F3", "#3F51B5", "#673AB7", "#9C27B0", "#E91E63"],
        dataLabels: {
          enabled: false
        },
        legend: {
          show: false
        },
        xaxis: {
          categories: ['0','0.5','1','2','3','5','8','13','20','40','100'],
          labels: {
            style: {
              colors: this.colors,
              fontSize: '12px'
            }
          }
        }
      },
      series2: [{
        name: "Mean",
        data: [0]
      }],
      chartOptions2:{
        chart: {
          height: 40,
          type: "bar",
          stacked: true,
          sparkline: {
            enabled: true
          }
        },
        plotOptions: {
          bar: {
            horizontal: true,
            barHeight: "20%",
            colors: {
              backgroundBarColors: ["#263238"]
            }
          }
        },
        colors: ["#F44336"],
        dataLabels: {
          enabled: true,
          textAnchor: 'start',
          style: {
            colors: ['#fff']
          },
          offsetX: 0,
        },
        stroke: {
          width: 0
        },
        tooltip: {
          enabled: true
        },
        xaxis: {
          categories: ["Mean"]
        },
        yaxis: {
          max: 100,
        },
        fill: {
          opacity: 1
        }
      }
    }
  },
  methods: {
    updateChart(index) {
      console.log('test', index)
      var newData = this.series[0].data
      newData[index] += 1
      this.series = [{data: newData}]

      var counts = 0
      var sum = 0
      var i =0
      this.series[0].data.forEach(element => {
        var value = this.chartOptions.xaxis.categories[i]
        counts += element
        sum += value * element
        i++
      });

      var newMean = [ counts != 0 ? sum / counts : 0]
      this.series2 = [{data: newMean}]

    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
img {
  height: 200px;
}
/* img:hover {
  height: 220px;
} */
</style>
