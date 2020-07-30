<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <sidebar />
    <div class="main-content">
      <div class="main-container">
        <div class="cb-row account-row">
          <stats-card class="cb-col-3" title="Total Seles" :value="totasales" />
          <stats-card class="cb-col-3" title="Total Trxns" :value="totalTrans" />
          <stats-card class="cb-col-4" title="Total Chgbks" :value="totalCbs" />
          <stats-card class="cb-col-4" title="% CB to Sales" value="2%" color="red" />
          <stats-card class="cb-col-4" title="% CB to Trxns" value=".12%" color="red" />
          <stats-card class="cb-col-3" title="Total CB Fees" value="$56,158,914" color="red" />
        </div>
        <div class="cb-row chart-row">
          <div class="paper-box">
            <div class="paper-box_head">
              <h3 class="cb-sub-title">Chargeback Overview</h3>
            </div>
            <div class="paper-box_content">
              <div class="cb-filter-group">
                <div class="cb-filter">
                  <div class="cb-filter_btn no-border">
                    <span class="cb-filter_text" @click="monthHandler()">{{selectedMonth}}</span>
                    <span class="arrow-icon"></span>
                  </div>
                  <ul class="cb-filter_list" v-if="showMonths">
                    <li
                      v-for="m in months"
                      :key="m"
                      class="cb-filter_item"
                      @click="selectMonth(m)"
                    >{{m}}</li>
                  </ul>
                </div>

                <div class="cb-filter data-picker">
                  <VueCtkDateTimePicker
                    buttonColor="#0892d0"
                    color="#1b2134"
                    id="RangeDatePicker"
                    range
                    v-model="dateRangeValue"
                    @validate="applyFilter($event)"
                  />
                  <div class="cb-filter_btn">
                    <span class="cb-filter_text">Range</span>

                    <span class="arrow-icon"></span>
                  </div>
                </div>
                <div class="cb-filter">
                  <div class="cb-filter_btn bg-blue">
                    <span class="cb-filter_text">Last</span>
                    <span class="arrow-icon white"></span>
                  </div>
                </div>
                <div class="cb-filter">
                  <div class="cb-filter_btn bg-blue">
                    <span class="cb-filter_text">Current</span>
                    <span class="arrow-icon white"></span>
                  </div>
                </div>

                <button class="cb-btn" v-on:click="applyFilter()">Today</button>
              </div>
              <overview :cbData="filteredData" />
            </div>
          </div>
        </div>
        <merchant-health :cbData="filteredData" />
        <cb-summary :cbData="filteredData" :columns="columns" />
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
import VueCtkDateTimePicker from "vue-ctk-date-time-picker";
import "vue-ctk-date-time-picker/dist/vue-ctk-date-time-picker.css";
// import VuetableFieldCheckbox from "vuetable-2/src/components/VuetableFieldCheckbox.vue";
export default {
  name: "ChargebackContainer",
  data: () => {
    return {
      cbData: [],
      filteredData: [],
      columns: [],
      dateRangeValue: null,
      months: [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December"
      ],
      showMonths: false,
      selectedMonth: "Month"
    };
  },
  components: {
    CbSummary,
    Overview,
    MerchantHealth,
    StatsCard,
    Sidebar,
    VueCtkDateTimePicker
  },

  mounted: function() {
    fetch("data.csv", { mode: "no-cors" })
      .then(response => response.text())
      .then(text => {
        const parsedData = this.csvJSON(text);
        this.cbData = JSON.parse(parsedData);
        this.filteredData = JSON.parse(parsedData);
        this.columns = this.getColomnNames(this.cbData);
      });
  },
  computed: {
    totasales: function() {
      const sales = this.filteredData.reduce((prev, cur) => {
        return (parseFloat(prev) + parseFloat(cur.cb_amt)).toFixed(2);
      }, 0);
      return `$${sales}`;
    },
    totalTrans: function() {
      const trans = this.filteredData.reduce((prev, cur) => {
        return (parseFloat(prev) + parseFloat(cur.tran_amt)).toFixed(2);
      }, 0);
      return `$${trans}`;
    },
    totalCbs: function() {
      const cash = this.filteredData.length;
      return `$${cash}`;
    }
  },
  methods: {
    csvJSON: function(csv) {
      let lines = csv.split("\n");
      let result = [];
      let headers = lines[0].split(",");
      for (var i = 1; i < lines.length; i++) {
        let obj = {};
        let currentline = lines[i].split(/,(?=(?:[^"]*"[^"]*")*(?![^"]*"))/);
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
          sortField: k
        };
        return obj;
      });

      return columns;
    },
    // eslint-disable-next-line no-unused-vars
    applyFilter: function(e) {
      const startDate = new Date(this.dateRangeValue.start);
      const endDate = new Date(this.dateRangeValue.end);
      const dataToFilter = this.cbData;
      const result = dataToFilter.filter(d => {
        const time = new Date(d.cb_date);
        return startDate < time && time < endDate;
      });

      this.filteredData = [...result];
    },
    monthHandler: function() {
      this.showMonths = !this.showMonths;
    },
    selectMonth: function(m) {
      this.selectedMonth = m;
      this.showMonths = !this.showMonths;
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
.chart-row {
  .cb-filter-group {
    .date-time-picker {
      position: absolute !important;
      top: 0;
      bottom: 0;
      height: 100%;
      width: 100%;
      left: 0;
      > div {
        &:first-child {
          opacity: 0;
          height: 100%;
        }
      }
    }
    .cb-filter {
      position: relative;
    }
  }
}

</style>
