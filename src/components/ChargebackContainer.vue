<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <cb-summary :cbData="cbData" :columns="columns" />
  </div>
</template>

<script>
import CbSummary from "./Summary";
export default {
  name: "ChargebackContainer",
  data: () => {
    return {
      cbData: [],
      columns: []
    };
  },
  components: {
    CbSummary
  },

  created: function() {
    fetch("data.csv", { mode: "no-cors" })
      .then(response => response.text())
      .then(text => {
        const parsedData = this.csvJSON(text);
        // console.log(parsedData);

        this.cbData = JSON.parse(parsedData);
        this.columns = this.getColomnNames(this.cbData);
        // console.log(parsedData)
      });
  },
  methods: {
    csvJSON: function(csv) {
      let lines = csv.split("\n");
      let result = [];
      let headers = lines[0].split(",");
      for (var i = 1; i < lines.length; i++) {
        let obj = {};
        let currentline = lines[i].split(",");
        for (let j = 0; j < headers.length; j++) {
          obj[headers[j]] = currentline[j];
        }
        result.push(obj);
      }
      return JSON.stringify(result); //JSON
    },
    getColomnNames: function(data) {
      const keys = Object.keys(data[0]);
      const columns = keys.map(k => {
        const obj = {
          title: k,
          name: k,
          sortField: k,
        };
        return obj;
      });
      return columns;
    }
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
