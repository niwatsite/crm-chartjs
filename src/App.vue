<template>
  <div id="app">
    <p class="title">Chart.jS Vue</p>
    <p>
      <canvas id="graph" width="1024" height="350"></canvas>
    </p>
  </div>
</template>

<script>
import Chart from "chart.js";
export default {
  components: {},
  mounted: () => {
    var ctx = document.getElementById("graph").getContext("2d");
    var myChart = new Chart(ctx, {
      type: "bar",
      data: {
        labels: [
          "Oui",
          "Nui",
          "Beer",
          "Opie",
          "Na",
          "Oum",
          "Air",
          "Pim",
          "Milk",
          "Mai",
          "Fon",
          "Do"
        ],
        datasets: [
          {
            label: "Call",
            backgroundColor: "#C4BEF2",
            data: [20, 59, 5, 56, 58, 12, 59, 87, 45, 2, 5, 6]
          },
          {
            label: "Email",
            backgroundColor: "#7C6BF7",
            data: [20, 59, 5, 56, 58, 12, 59, 85, 23, 24, 5, 6]
          },
          {
            label: "Meeting",
            backgroundColor: "#5847D7",
            data: [35, 59, 5, 56, 58, 12, 59, 65, 51, 2, 59, 6]
          }
        ]
      },
      options: {
        // tooltips: {
        //   mode: "index",
        //   intersect: false,
        // },
        tooltips: {
          mode: "label",
          backgroundColor:"rgb(255,255,255)",
          titleFontColor:"#7C818D",
          bodyFontColor:"#272E39",
          footerFontColor:"#272E39",
          callbacks: {
            afterTitle: () => (window.total = 0),
            label: (tooltipItem, data) => {
              let corporation = data.datasets[tooltipItem.datasetIndex].label;
              let valor =
                data.datasets[tooltipItem.datasetIndex].data[tooltipItem.index];
              window.total += valor;
              return (
                corporation +
                ": " +
                valor.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
              );
            },
            footer: () =>
              "Total: " +
              window.total.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
          }
        },
        scales: {
          xAxes: [
            {
              stacked: true,
              gridLines: {
                display: false
              }
            }
          ],
          yAxes: [
            {
              stacked: true,
              ticks: {
                beginAtZero: true
              },
              type: "linear"
            }
          ]
        },
        responsive: true,
        maintainAspectRatio: false,
        defaultFontFamily: "'Sarabun Regular'",
        title: {
          display: true,
          fontSize: 14,
          position: "left",
          text: "Number of activities"
        },
        legend: {
          position: "bottom",
          labels: { usePointStyle: true, boxWidth: 10, padding: 50 }
        }
      }
    });
    console.log(myChart);
  },
  data() {
    return {};
  }
};
</script>

<style>
html {
  height: 100%;
}
body {
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100%;
}
</style>
