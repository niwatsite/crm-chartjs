<template>
  <div id="app">
    <p class="title">Chart.jS Vue</p>
    <p>
      <canvas ref="graph" id="graph" width="1024" height="350"></canvas>
    </p>
    <p>
      <a
        id="download"
        @click="download"
        download="ChartImage.jpg"
        title="Descargar Gráfico"
      >
        Download
      </a>
    </p>
  </div>
</template>

<script>
import Chart from "chart.js";
export default {
  components: {},
  mounted: () => {
    const ctx = document.getElementById("graph").getContext("2d");
    const myChart = new Chart(ctx, {
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
            data: [20, 30, 5, 56, 58, 12, 59, 85, 23, 24, 5, 6]
          },
          {
            label: "Meeting",
            backgroundColor: "#5847D7",
            data: [35, 35, 5, 56, 58, 12, 59, 65, 51, 2, 59, 6]
          }
        ]
      },
      options: {
        tooltips: {
          mode: "label",
          backgroundColor: "rgb(255,255,255)",
          titleFontColor: "#7C818D",
          bodyFontColor: "#272E39",
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
            }
            // afterTitle: () =>
            //   "Total: " +
            //   window.total.toString().replace(/\B(?=(\d{3})+(?!\d))/g, " ")
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
    return {
      item: [
        {
          name: "Oui",
          items: [
            {
              kay: "Call",
              value: 20
            },
            {
              kay: "Email",
              value: 29
            }
          ]
        },
        {
          name: "Nui",
          items: [
            {
              kay: "Call",
              value: 30
            },
            {
              kay: "Email",
              value: 35
            }
          ]
        }
      ]
    };
  },
  methods: {
    download() {
      /*Get image of canvas element*/
      const url_base64jp =
        //document
        //.getElementById("graph")
        this.$refs.graph.toDataURL("image/jpg");
      /*get download button (tag: <a></a>) */
      let a = document.getElementById("download");
      /*insert chart image url to download button (tag: <a></a>) */
      a.href = url_base64jp;
    }
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

a {
  color: red;
  width: 100px;
  height: 30px;
}
</style>
