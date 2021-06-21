<template>
  <h2>hello</h2>
  <div v-if="tableData.length == 0">Table is empty</div>
  <div v-else>
    <div class="table-container">
      <table>
        <thead>
          <tr>
            <th>Title</th>
            <th>Start</th>
            <th>End</th>
            <th>Num Voters</th>
            <th>Unique Holders</th>
            <th>vMTA voted</th>
            <th>vMTA total</th>
            <th>State</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="data in tableData" :key="data._id">
            <td>{{ data.title }}</td>
            <td>{{ data.start }}</td>
            <td>{{ data.end }}</td>
            <td>{{ data.votersNum }}</td>
            <td>{{ data.votersTotal }}</td>
            <td>{{ data.scoreNum }}</td>
            <td>{{ data.scoreTotal }}</td>
            <td>{{ data.state }}</td>
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
/* .styled-table {
  border-collapse: collapse;
  margin: 25px 0;
  font-size: 0.9em;
  font-family: sans-serif;
  min-width: 400px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.15);
}
.styled-table thead tr {
  background-color: #009879;
  color: #ffffff;
  text-align: left;
}
.styled-table th,
.styled-table td {
  padding: 12px 15px;
}
.styled-table tbody tr {
  border-bottom: 1px solid #dddddd;
}
.styled-table tbody tr:nth-of-type(even) {
  background-color: #f3f3f3;
}
.styled-table tbody tr:last-of-type {
  border-bottom: 2px solid #009879;
}
.styled-table tbody tr.active-row {
  font-weight: bold;
  color: #009879;
} */

.table-container {
  position: relative;
  overflow: auto;
  height: 80vh;
  border: 1px solid rgba(23, 110, 222, 0.5);
  box-shadow: rgb(0 0 0 / 5%) 0px 4px 12px;
}
table {
  border-collapse: collapse;
  table-layout: fixed;
}
td,
th {
  border: 1px solid rgba(23, 110, 222, 0.5);
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
  background: rgb(23, 110, 222);
  border-top: none;
  border-bottom: none;
  color: #fff;
}
thead th:first-child {
  left: -1px;
  z-index: 3;
  border-left: none;
}
tbody tr > :first-child {
  position: -webkit-sticky;
  position: sticky;
  background: #f7f7f7;
  left: 0;
  border-left: none;
}
tbody tr:last-child td {
  border-bottom: none;
}
</style>
