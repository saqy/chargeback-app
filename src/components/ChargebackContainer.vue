<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <sidebar/>
    <div class="main-content">
      <div class="main-container">
      <stats-card/>
          <div class="cb-row chart-row">
              <div class="paper-box">
                  <div class="paper-box_head">
                      <h3 class="cb-sub-title">Chargeback Overview</h3>
                  </div>
                  <div class="paper-box_content">
                      <div class="cb-filter-group">
                          <div class="cb-filter">
                              <div class="cb-filter_btn no-border">
                                  <span class="cb-filter_text">Month</span>
                                  <span class="arrow-icon">
                                  </span>
                              </div>
                              <ul class="cb-filter_list">
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                              </ul>
                          </div>
                          <div class="cb-filter">
                              <div class="cb-filter_btn">
                                  <span class="cb-filter_text">Range</span>
                                  <span class="arrow-icon">
                                  </span>
                              </div>
                              <ul class="cb-filter_list">
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                              </ul>
                          </div>
                          <div class="cb-filter">
                              <div class="cb-filter_btn bg-blue">
                                  <span class="cb-filter_text">Last</span>
                                  <span class="arrow-icon white">
                                  </span>
                              </div>
                              <ul class="cb-filter_list">
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                              </ul>
                          </div>
                          <div class="cb-filter">
                              <div class="cb-filter_btn bg-blue">
                                  <span class="cb-filter_text">Current</span>
                                  <span class="arrow-icon white">
                                  </span>
                              </div>
                              <ul class="cb-filter_list">
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                              </ul>
                          </div>

                          <button class="cb-btn">
                              Today
                          </button>
                      </div>
                      <overview />
                  </div>
              </div>
          </div>
          <merchant-health />
          <cb-summary :cbData="cbData" :columns="columns" />
      </div>
    </div>
  </div>
</template>

<script>
import CbSummary from "./Summary";
import Overview from "./Overview";
import MerchantHealth from "./MerchantHealth";
import StatsCard from "./StatsCard";
import Sidebar from "./Sidebar";
export default {
  name: "ChargebackContainer",
  data: () => {
    return {
      cbData: [],
      columns: []
    };
  },
  components: {
    CbSummary,
    Overview,
    MerchantHealth,
    StatsCard,
    Sidebar
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
        let currentline = lines[i].split(/,(?=(?:[^"]*"[^"]*")*(?![^"]*"))/)
        for (let j = 0; j < headers.length; j++) {
          obj[headers[j]] = currentline[j].replace(/"/g, "");
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

<style lang="scss">
@import "../assets/variable.scss";
@import "../assets/global.scss";
.main-content {
    flex: 1;
    background-color: $gray;
    width: calc(100% - 340px);
    margin-left: 340px;
    @media screen and (max-width: 1900px) {
        width: calc(100% - 300px);
        margin-left: 300px;
    }
    @media screen and (max-width: 1599px) {
        width: calc(100% - 280px);
        margin-left: 280px;
    }
    @media screen and (max-width: 1279px) {
        width: 100%;
        margin-left: 0;
    }
}
.merchant-row {
    .paper-box_head {
        padding-left: 30px;
        padding-right: 30px;
        border-color: #e1e7f0;
        .cb-sub-title {
            margin-bottom: 0;
        }
    }
}
</style>
