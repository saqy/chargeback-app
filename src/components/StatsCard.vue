<template>
   <div class="cb-row account-row">
        <div class="cb-col-3">
            <div class="paper-box">
                <div class="paper-box_head">
                    <h3 class="cb-sub-title">Total Seles</h3>
                </div>
                <div class="paper-box_content">
                    <span class="text-blue">$56,158,914</span>
                </div>
            </div>
        </div>
        <div class="cb-col-3">
            <div class="paper-box">
                <div class="paper-box_head">
                    <h3 class="cb-sub-title">Total Trxns</h3>
                </div>
                <div class="paper-box_content">
                    <span class="text-blue">36,158,914</span>
                </div>
            </div>
        </div>
        <div class="cb-col-4">
            <div class="paper-box">
                <div class="paper-box_head">
                    <h3 class="cb-sub-title">Total Chgbks</h3>
                </div>
                <div class="paper-box_content">
                    <span class="text-blue">1,914</span>
                </div>
            </div>
        </div>
        <div class="cb-col-4">
            <div class="paper-box">
                <div class="paper-box_head">
                    <h3 class="cb-sub-title">% CB to Sales</h3>
                </div>
                <div class="paper-box_content">
                    <span class="text-red">2%</span>
                </div>
            </div>
        </div>
        <div class="cb-col-4">
            <div class="paper-box">
                <div class="paper-box_head">
                    <h3 class="cb-sub-title">% CB to Trxns</h3>
                </div>
                <div class="paper-box_content">
                    <span class="text-red">.12%</span>
                </div>
            </div>
        </div>
        <div class="cb-col-3">
            <div class="paper-box">
                <div class="paper-box_head">
                    <h3 class="cb-sub-title">Total CB Fees</h3>
                </div>
                <div class="paper-box_content">
                    <span class="text-red">$56,158,914</span>
                </div>
            </div>
        </div>
    </div>
</template>

<script>


export default {
  name: "StatsCard",

  components: {

  },

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
  watch: {
 
  },
  data() {
    return {
      data: [],
    };
  },
  methods: {

  }
};
</script>

<style lang="scss">
@import "../assets/global.scss";
.account-row {
        margin-left: -8px;
        margin-right: -8px;
        @media screen and (max-width: 991px) {
            flex-wrap: wrap;
        }
        .cb-col-4 {
            max-width: 22%;
            flex: 22%;
            padding: 0 8px;
            @media screen and (max-width: 991px) {
                max-width: 33.33%;
                flex: 33.33%;
                margin-top: 15px;
            }
            @media screen and (max-width: 479px) {
                max-width: 50%;
                flex: 50%;
            }
        }
        .cb-col-3 {
            max-width: 28%;
            flex: 28%;
            padding: 0 8px;
            @media screen and (max-width: 991px) {
                max-width: 33.33%;
                flex: 33.33%;
                margin-top: 15px;
            }
            @media screen and (max-width: 479px) {
                max-width: 50%;
                flex: 50%;
            }
        }
        .paper-box {
            height: 100%;
        }
        .paper-box_head {
            border-color: #838384;
            padding-left: 20px;
            padding-right: 20px;
            @media screen and (max-width: 1900px) {
                padding-left: 12px;
                padding-right: 12px;
            }
        }
        .paper-box_content {
            padding: 40px 20px;
            font-size: 38px;
            font-weight: 900;
            @media screen and (max-width: 1900px) {
                padding: 34px 12px;
                font-size: 26px;
            }
            @media screen and (max-width: 767px) {
                padding: 20px 12px;
                font-size: 18px;
            }
        }
        .cb-sub-title {
            @media screen and (max-width: 1900px) {
                font-size: 16px;
            }
            @media screen and (max-width: 1599px) {
                font-size: 15px;
            }
        }
    }
</style>
