<template>
  <h2>hello</h2>
  <div v-if="!tableData.length">Table is empty</div>
  <div v-else>
    <table class="styled-table">
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
</template>

<script>
export default {
  name: "Table",
  props: ["data"],
  setup(props) {
    console.log(props.data[0].keys);

    return { tableData: props.data };
  },
};
</script>

<style>
.styled-table {
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
}
</style>
