<template>
  <div v-if="tableData.length == 0">Table is empty</div>
  <div v-else>
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
            <td class="col-highlight">
              {{ ((data.votersNum / data.votersTotal) * 100).toFixed(2) }}%
            </td>

            <td>{{ data.scoreNum.toFixed(2) }}</td>
            <td>{{ data.scoreTotal.toFixed(2) }}</td>
            <td class="col-highlight">
              {{ ((data.scoreNum / data.scoreTotal) * 100).toFixed(2) }}%
            </td>
            <!-- <td>{{ data.state }}</td> -->
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  name: "Table",
  props: ["data"],
  setup(props) {
    return { tableData: props.data };
  },
};
</script>

<style>
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
