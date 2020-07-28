<template>
   <div class="cb-row merchant-row">
        <div class="paper-box">
            <div class="paper-box_head">
                <h3 class="cb-sub-title">Merchant Health</h3>
            </div>
            <div class="paper-box_content">
                <div class="sub-container">
                    <div class="cb-col">
                        <div class="box">
                            <h3 class="cb-sub-title">T1</h3>
                            <span class="cb-badge bg-pink">UNHEALTHY</span>
                            <div class="cb-account-box">
                                <span class="label">Total Sales</span>
                                <span class="value">$6,158,914</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Transactions</span>
                                <span class="value">$4,158,900</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Chargebacks</span>
                                <span class="value">684</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-mix-gradient"></div>
                                </div>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Total Sales</span>
                                <span class="value">25%</span>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Transactions</span>
                                <span class="value">12%</span>
                            </div>
                            
                        </div>
                    </div>
                    <div class="cb-col">
                        <div class="box">
                            <h3 class="cb-sub-title">Metropolitan</h3>
                            <span class="cb-badge bg-green">UNHEALTHY</span>
                            <div class="cb-account-box">
                                <span class="label">Total Sales</span>
                                <span class="value">$6,158,914</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Transactions</span>
                                <span class="value">$4,158,900</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Chargebacks</span>
                                <span class="value">684</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-mix-gradient"></div>
                                </div>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Total Sales</span>
                                <span class="value">25%</span>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Transactions</span>
                                <span class="value">12%</span>
                            </div>
                            
                        </div>
                    </div>
                    <div class="cb-col">
                        <div class="box">
                            <h3 class="cb-sub-title">Payarc</h3>
                            <span class="cb-badge bg-orange">UNHEALTHY</span>
                            <div class="cb-account-box">
                                <span class="label">Total Sales</span>
                                <span class="value">$6,158,914</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Transactions</span>
                                <span class="value">$4,158,900</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Chargebacks</span>
                                <span class="value">684</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-mix-gradient"></div>
                                </div>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Total Sales</span>
                                <span class="value">25%</span>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Transactions</span>
                                <span class="value">12%</span>
                            </div>
                            
                        </div>
                    </div>
                    <div class="cb-col">
                        <div class="box">
                            <h3 class="cb-sub-title">ProPay</h3>
                            <span class="cb-badge bg-pink">UNHEALTHY</span>
                            <div class="cb-account-box">
                                <span class="label">Total Sales</span>
                                <span class="value">$6,158,914</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Transactions</span>
                                <span class="value">$4,158,900</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-blue-gradient-h"></div>
                                </div>
                            </div>
                            <div class="cb-account-box">
                                <span class="label">Total Chargebacks</span>
                                <span class="value">684</span>
                                <div class="cb-progress">
                                    <div class="cb-progress-bar bg-mix-gradient"></div>
                                </div>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Total Sales</span>
                                <span class="value">25%</span>
                            </div>
                            <div class="cb-account-percentage">
                                <span class="label">% of Transactions</span>
                                <span class="value">12%</span>
                            </div>
                            
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>


export default {
  name: "MerchantHealth",

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
@import "../assets/variable.scss";
.merchant-row {
        .sub-container {
            max-width: 1430px;
            margin: 0 auto;
            display: flex;
            justify-content: space-between;
            padding: 60px 15px;
            @media screen and (max-width: 767px) {
                flex-wrap: wrap;
                padding: 40px 15px 10px;
            }
        }
        .cb-badge {
            color: #fff;
            padding: 4px 10px;
            border-radius: 30px;
            font-size: 10px;
            margin-bottom: 8px;
            display: inline-block;
        }
        .cb-col {
            max-width: 242px;
            flex: 242px;
            padding-right: 15px;
            @media screen and (max-width: 767px) {
                max-width: 50%;
                flex: 50%;
                margin-bottom: 30px;
            }
            @media screen and (max-width: 479px) {
                max-width: 100%;
                flex: 100%;
                margin-bottom: 25px;
                padding-bottom: 15px;
                border-bottom: 1px solid #ddd;
                padding-right: 0;
                &:last-child {
                    border-bottom: 0;
                }
            }
        }
        .cb-sub-title {
            margin-bottom: 8px;
        }
        .cb-account-box {
            display: flex;
            flex-direction: column;
            .label {
                display: inline-block;
                color: $primaryText;
                margin-bottom: 5px;
                font-size: 20px;
                font-weight: 600;
                @media screen and (max-width: 1599px) {
                    font-size: 18px;
                }
                @media screen and (max-width: 991px) {
                    font-size: 16px;
                }
            }
            .value {
                display: inline-block;
                color: $primaryText;
                font-size: 30px;
                font-weight: 900;
                margin-bottom: 3px;
                @media screen and (max-width: 1599px) {
                    font-size: 26px;
                }
                @media screen and (max-width: 991px) {
                    font-size: 21px;
                }
            }
            .cb-progress {
                height: 24px;
                margin-bottom: 15px;
                background-color: #e4ebf7;
                @media screen and (max-width: 1599px) {
                    height: 21px
                }
                @media screen and (max-width: 991px) {
                    height: 19px
                }
                .cb-progress-bar {
                    height: 100%;
                    width: 75%;
                    background-color: $lightBlue;
                }
            }
        }
        .cb-account-percentage {
            display: flex;
            flex-direction: column;
            .label {
                display: inline-block;
                color: $primaryText;
                margin-bottom: 5px;
                font-size: 14px;
                font-weight: 500;
            }
            .value {
                display: inline-block;
                color: $lightBlue;
                font-size: 22px;
                font-weight: 900;
                margin-bottom: 8px;
            }
        }
    }

</style>
