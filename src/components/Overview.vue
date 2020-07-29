<template>
  <div class="chart-wrapper">
    <div class="chart-info">
      <ul class="chart-info_list">
        <li class="chart-info_item">
          <span class="color-identity bg-blue-gradient-v"></span>
          <span class="text">Total Sales</span>
        </li>
        <li class="chart-info_item">
          <span class="color-identity bg-yellow"></span>
          <span class="text">Total Chgbk</span>
        </li>
      </ul>
      <div id="chartContainer" style="height: 300px; width: 100%;"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Overview",

  components: {},

  props: {
    cbData: {
      type: Array,
      required: true
    },
    columns: {
      type: Array,
      required: true
    }
  },
  watch: {},
  data() {
    return {
      data: []
    };
  },
  mounted: function() {
    window.onload = function() {
      var options = {
        animationEnabled: true,
        theme: "light2",
        title: {
          text: "Monthly Sales Data"
        },
        axisX: {
          valueFormatString: "MMM"
        },
        axisY: {
          prefix: "$"
        },
        toolTip: {
          shared: true
        },
        legend: {
          cursor: "pointer"
        },
        data: [
          {
            type: "area",
            name: "Profit",
            markerBorderColor: "white",
            markerBorderThickness: 2,
            showInLegend: true,
            yValueFormatString: "$#,##0",
            dataPoints: [
              { x: new Date(2017, 0), y: 4000 },
              { x: new Date(2017, 1), y: 7000 },
              { x: new Date(2017, 2), y: 12000 },
              { x: new Date(2017, 3), y: 40000 },
              { x: new Date(2017, 4), y: 20000 },
              { x: new Date(2017, 5), y: 35000 },
              { x: new Date(2017, 6), y: 33000 },
              { x: new Date(2017, 7), y: 20000 },
              { x: new Date(2017, 8), y: 25000 },
              { x: new Date(2017, 9), y: 16000 },
              { x: new Date(2017, 10), y: 29000 },
              { x: new Date(2017, 11), y: 20000 }
            ]
          },
          {
            type: "area",
            name: "Profit",
            markerBorderColor: "white",
            markerBorderThickness: 2,
            showInLegend: true,
            yValueFormatString: "$#,##0",
            dataPoints: [
              { x: new Date(2017, 0), y: 5000 },
              { x: new Date(2017, 1), y: 7000 },
              { x: new Date(2017, 2), y: 15000 },
              { x: new Date(2017, 3), y: 4000 },
              { x: new Date(2017, 4), y: 2000 },
              { x: new Date(2017, 5), y: 37000 },
              { x: new Date(2017, 6), y: 34000 },
              { x: new Date(2017, 7), y: 21000 },
              { x: new Date(2017, 8), y: 23000 },
              { x: new Date(2017, 9), y: 17000 },
              { x: new Date(2017, 10), y: 29000 },
              { x: new Date(2017, 11), y: 21000 }
            ]
          }
        ]
      };
      console.log('window.$');
      console.log(window.$);
      window.$("#chartContainer").CanvasJSChart(options);
    };
  },

  methods: {}
};
</script>

<style lang="scss">
@import "../assets/variable.scss";
.chart-row {
  .paper-box_head {
    padding-left: 30px;
    padding-right: 30px;
    border-color: #e1e7f0;
  }
  .cb-filter-group {
    padding-top: 36px;
    display: flex;
    padding-left: 56px;
    padding-right: 56px;
    @media screen and (max-width: 1599px) {
      padding-left: 30px;
      padding-right: 30px;
    }
    @media screen and (max-width: 991px) {
      padding-left: 20px;
      padding-right: 20px;
    }
    @media screen and (max-width: 767px) {
      flex-wrap: wrap;
    }
    @media screen and (max-width: 479px) {
      padding-top: 15px;
    }
    .cb-btn {
      margin-left: auto;
      @media screen and (max-width: 767px) {
        margin-left: 0;
      }
    }
    .cb-filter {
      margin-right: 35px;
      @media screen and (max-width: 991px) {
        margin-right: 20px;
      }
      @media screen and (max-width: 767px) {
        margin-bottom: 10px;
      }
      &:last-child {
        margin-right: 0;
      }
    }
  }
  .chart-wrapper {
    min-height: 650px;
    padding-left: 30px;
    padding-right: 30px;
    position: relative;
    @media screen and (max-width: 767px) {
      min-height: 330px;
    }
    .chart-info {
      &_list {
        display: block;
        position: absolute;
        left: 88px;
        top: 40px;
        @media screen and (max-width: 1599px) {
          left: 52px;
        }
        @media screen and (max-width: 767px) {
          left: 30px;
        }
      }
      &_item {
        padding: 10px 0;
        display: flex;
        .text {
          font-size: 20px;
          font-weight: 600;
          color: $primaryText;
          @media screen and (max-width: 767px) {
            font-size: 17px;
          }
        }
        .color-identity {
          display: block;
          height: 28px;
          width: 28px;
          margin-right: 15px;
          @media screen and (max-width: 767px) {
            height: 20px;
            width: 20px;
            margin-right: 10px;
          }
        }
      }
    }
  }
}
</style>
