<template>
  <div id="app">
    <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
    <sidebar />
    <div class="main-content">
      <div class="main-container">
        <stats-card />
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
                    <span class="arrow-icon"></span>
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
                  <!-- <ul class="cb-filter_list">
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                                  <li class="cb-filter_item">Item</li>   
                  </ul> -->
                </div>
                <div class="cb-filter">
                  <div class="cb-filter_btn bg-blue">
                    <span class="cb-filter_text">Last</span>
                    <span class="arrow-icon white"></span>
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
                    <span class="arrow-icon white"></span>
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

                <button class="cb-btn">Today</button>
              </div>
              <overview />
            </div>
          </div>
        </div>
        <merchant-health />
        <cb-summary :cbData="filteredData" :columns="columns" />
      </div>
    </div>
    <div class="modal-wrapper">
        <div class="paper-box">
            <div class="paper-box_head">
                <h3 class="cb-sub-title">Calculation Results</h3>
            </div>
            <div class="paper-box_content">
                <div class="model-content">
                    <div class="model-row">
                        <span class="label">Total CB</span>
                        <span class="value">1,194</span>
                    </div>
                    <div class="model-row">
                        <span class="label">Total QV</span>
                        <span class="value">1,194</span>
                    </div>
                    <div class="model-row">
                        <span class="label">Total CV</span>
                        <span class="value">1,194</span>
                    </div>
                    <div class="model-row">
                        <span class="label">Total Amount</span>
                        <span class="value">1,194</span>
                    </div>
                    <div class="model-row">
                        <span class="label">Total CB Fees</span>
                        <span class="value">1,194</span>
                    </div>
                    <div class="btn-group">
                        <button class="cb-btn bg-blue">Export</button>
                        <button class="cb-btn bg-blue">Close</button>
                    </div>
                </div>
            </div>
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
export default {
  name: "ChargebackContainer",
  data: () => {
    return {
      cbData: [],
      filteredData: [],
      columns: [],
      dateRangeValue: null
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

  mounted: function (){
    fetch("data.csv", { mode: "no-cors" })
      .then(response => response.text())
      .then(text => {
        const parsedData = this.csvJSON(text);
        // console.log(parsedData);

        this.cbData = JSON.parse(parsedData);
        this.filteredData = JSON.parse(parsedData);
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
      console.log("here..");
      console.log(this.dateRangeValue); 
      const startDate = new Date(this.dateRangeValue.start);
      const endDate = new Date(this.dateRangeValue.end);
      const dataToFilter=this.cbData;
      const result = dataToFilter.filter(d => {
          console.log('d')
          console.log(d)
        const time = new Date(d.cb_date);
        return startDate < time && time < endDate;
      });
   
     this.filteredData = [...result];
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
      position: absolute;
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
  }
}
.modal-wrapper {
    display: none;
    width: 100%;
    height: 100%;
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    top: 0;
    background-color: rgba(0, 0, 0, 0.3);
    z-index: 9999;
    .paper-box {
        max-width: 600px;
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        @media screen and (max-width: 639px) {
            left: 20px;
            right: 20px;
            transform: translate(0, -50%);
            width: calc(100% - 40px)
        }
        &_head {
            border-color: lightblue;
            padding-left: 20px;
            padding-right: 20px;
        }
        &_content {
            padding: 40px;
            .model-content {
                max-width: 400px;
                margin: 0 auto;
            }
        }
        .model-row {
            display: flex;
            align-items: center;
            justify-content: space-between;
            span {
                font-size: 28px;
                font-weight: bold;
                color: $primaryText;
                padding: 8px 0;
                @media screen and (max-width: 767px) {
                    font-size: 20px;
                }
            }
        }
        .btn-group {
            display: flex;
            justify-content: center;
            margin-top: 40px;
            .cb-btn {
                height: 50px;
                margin: 0 10px;
                @media screen and (max-width: 767px) {
                    height: 36px;
                }
            }
        }
    }
}
</style>
