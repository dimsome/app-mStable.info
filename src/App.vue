<template>
  <h1>mStable - Voting Participation</h1>
  <div v-if="error">{{ error }}</div>
  <div v-else>
    <div v-if="data.length">
      <Table :data="data" />
    </div>
    <div v-else>Loading</div>
  </div>
</template>

<script>
import Table from "./components/Table.vue";
import { ref } from "vue";

export default {
  name: "App",
  components: {
    Table,
  },
  setup() {
    const data = ref([]);
    const error = ref(null);

    const fetchData = async () => {
      try {
        let response = await fetch("http://127.0.0.1:4000/api/proposals");
        // console.log(response);
        if (!response.ok) throw Error("Data not fetched");
        data.value = await response.json();
      } catch (err) {
        error.value = err.message;
      }
    };

    fetchData();

    return { data, error };
  },
};
</script>

<style>
body {
  font-family: Poppins, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: rgb(37, 39, 45);
  margin-top: 60px;
  background: #f8f5f2;
}
</style>
