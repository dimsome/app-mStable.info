<template>
  <div v-if="tableData.length == 0">Table is empty</div>
  <div v-else>
    <div class="chart-container">
      <LineChart :chartData="chartData" :height="550" />
    </div>
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Title</th>
            <!-- <th>Start</th> -->
            <th>End</th>
            <th>Num Voters</th>
            <th>Total Holders</th>
            <th>Voter Percent</th>
            <th>vMTA voted</th>
            <th>vMTA total</th>
            <th>vMTA Percent</th>
            <!-- <th>State</th> -->
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in tableData" :key="data._id">
            <td>{{ data.title }}</td>
            <!-- <td>{{ data.start }}</td> -->
            <td>{{ data.end }}</td>
            <td>{{ data.votersNum }}</td>
            <td>{{ data.votersTotal }}</td>
            <td class="col-highlight">{{ data.percentNum }}%</td>
            <td>{{ data.scoreNum }}</td>
            <td>{{ data.scoreTotal }}</td>
            <td class="col-highlight">{{ data.percentScore }}%</td>
            <!-- <td>{{ data.state }}</td> -->
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { onMounted, ref } from "@vue/runtime-core";
import LineChart from "./LineChart";
export default {
  name: "Table",
  props: ["data"],
  components: {
    LineChart,
  },
  setup(props) {
    let dataPoints;

    const tableData = ref([]);
    const chartData = ref({});

    onMounted(() => {
      dataPoints = props.data.length;
      dataPoints = {
        labels: Array(dataPoints),
        datasets: [
          {
            label: "Percentage of vMTA holders voted",
            data: Array(dataPoints - 1),
            color: "#0061E3",
            borderColor: "#0061E3",
          },
          {
            label: "Percentage of vMTA score voted",
            data: Array(dataPoints - 1),
            borderColor: "#FAB41F",
          },
        ],
      };
      props.data.forEach((row, index) => {
        let percentNum = ((row.votersNum / row.votersTotal) * 100).toFixed(2);
        let percentScore = ((row.scoreNum / row.scoreTotal) * 100).toFixed(2);

        tableData.value.push({
          _id: row._id,
          title: row.title,
          end: row.end,
          votersNum: row.votersNum,
          votersTotal: row.votersTotal,
          percentNum,
          scoreNum: row.scoreNum.toFixed(2),
          scoreTotal: row.scoreTotal.toFixed(2),
          percentScore,
        });

        chartData.value.labels[dataPoints - index] = row.end;
        chartData.value.datasets[0].data[dataPoints - index] = percentNum;
        chartData.value.datasets[1].data[dataPoints - index] = percentScore;
      });
    });

    return { tableData, chartData };
  },
};
</script>

<style>
.chart-container {
  width: 100%;
  height: 600px;
}
.table-container {
  position: relative;
  overflow: auto;
  height: 80vh;
  border: 1px solid rgba(23, 110, 222, 0.5);
  box-shadow: rgb(0 0 0 / 5%) 0px 4px 12px;
}
.col-highlight {
  background: rgba(23, 110, 222, 0.05);
}
table {
  border-collapse: collapse;
  table-layout: fixed;
}
td,
th {
  border: 1px solid rgba(23, 110, 222, 0.75);
  border-top: none;
  padding: 10px;
  min-width: 200px;
  background: white;
  box-sizing: border-box;
  text-align: center;
}
thead th {
  position: -webkit-sticky;
  position: sticky;
  top: -1px;
  z-index: 2;
  background: rgb(23, 110, 222, 1);
  border-top: none;
  border-bottom: none;
  color: #fff;
}
thead th:first-child {
  left: -1px;
  z-index: 3;
  border-left: none;
  text-align: left;
}
tbody tr > :first-child {
  position: -webkit-sticky;
  position: sticky;
  background: #f7f7f7;
  left: 0;
  border-left: none;
  text-align: left;
}
tbody tr:last-child td {
  border-bottom: none;
}
</style>
