<template>
   
  <div id="app" class="ui container table-content-row">
    <!-- <input v-model="perPage" type="number" />
    <template>
      <select v-model="selectedCategory">
        <option
          v-for="option in columns"
          v-bind:value="option.name"
          :key="option.name"
        >{{ option.name }}</option>
      </select>
    </template> -->
    <div class="cb-filter-group">
        <div class="cb-checkbox">
            <input class="checkbox" type="checkbox" id="checkbox1">
            <label class="label" for="checkbox1">
                <div class="check-mark">
                </div>
            </label>
        </div>

        <div class="show-entries">
            <span class="label">show</span>
            <div class="entries-count">
                <input v-model="perPage" type="number" value="10">
                <div class="entries-btns">
                    <button class="up-btn">
                    </button>
                    <button class="down-btn">
                    </button>
                </div>
            </div>
            <span class="label">Entries</span>
        </div>

        
        <div class="cb-filter">
            <div class="cb-filter_btn bg-gray">
                <span class="cb-filter_text">Actions</span>
                <span class="arrow-icon">
                </span>
            </div>
            <ul class="cb-filter_list">
                <li class="cb-filter_item"
                v-for="option in columns"
                v-bind:value="option.name"
                :key="option.name"
                >{{ option.name }}</li>   
            </ul>
        </div>
        <button class="cb-btn bg-blue">
            Submit
        </button>

        <div class="cb-filter ml-auto">
            <div class="cb-filter_btn bg-gray">
                <span class="cb-filter_text">Filter</span>
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
        <button class="cb-btn bg-blue">
            Export CSV
        </button>
    </div>
    <div class="table-responsive">
      <vuetable
        ref="vuetable"
        :api-mode="false"
        :fields="columns"
        :per-page="perPage"
        :data-manager="dataManager"
        pagination-path="pagination"
        @vuetable:pagination-data="onPaginationData"
      >
        <div slot="actions" slot-scope="props">
          <button class="ui small button" @click="onActionClicked('view-item', props.rowData)">
            <i class="zoom icon"></i>
          </button>
          <button class="ui small button" @click="onActionClicked('edit-item', props.rowData)">
            <i class="edit icon"></i>
          </button>
          <button class="ui small button" @click="onActionClicked('delete-item', props.rowData)">
            <i class="delete icon"></i>
          </button>
        </div>
      </vuetable>
    </div>
    <div class="cb-pagination">
      <vuetable-pagination ref="pagination" @vuetable-pagination:change-page="onChangePage"></vuetable-pagination>
    </div>
  </div>
</template>

<script>
import Vuetable from "vuetable-2";
import VuetablePagination from "vuetable-2/src/components/VuetablePagination";

import _ from "lodash";

export default {
  name: "Summary",

  components: {
    Vuetable,
    VuetablePagination
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
    cbData: function(newVal) {
      this.data = newVal;
      this.$refs.vuetable.refresh();
    },
     perPage: function() {
      this.$nextTick(function() {
        this.$refs.vuetable.refresh()
      })
    },
    // data: function() {
    //   this.$refs.vuetable.refresh();
    // }
  },
  data() {
    return {
      data: [],
      perPage: 2,
      selectedCategory: ""
    };
  },
  methods: {
    onPaginationData(paginationData) {
      this.$refs.pagination.setPaginationData(paginationData);
    },
    onChangePage(page) {
      console.log(this.perPage);
      this.$refs.vuetable.changePage(page);
    },
    dataManager(sortOrder, pagination) {
      if (this.data.length < 1) return;

      let local = this.data;

      // sortOrder can be empty, so we have to check for that as well
      if (sortOrder.length > 0) {
        console.log("orderBy:", sortOrder[0].sortField, sortOrder[0].direction);
        local = _.orderBy(
          local,
          sortOrder[0].sortField,
          sortOrder[0].direction
        );
      }

      pagination = this.$refs.vuetable.makePagination(
        local.length,
        this.perPage
      );
      console.log("pagination:", pagination);
      let from = pagination.from - 1;
      let to = from + this.perPage;

      return {
        pagination: pagination,
        data: _.slice(local, from, to)
      };
    },
    onActionClicked(action, data) {
      console.log("slot actions: on-click", data.name);
    }
    // onItemsPerPageChange(){
    //   this.perPage= itemsPerPage;

    // }
  }
};
</script>

<style lang="scss">
@import "../assets/global.scss";
.table-content-row {
        .paper-box_head {
            padding-left: 30px;
            padding-right: 30px;
            border-color: transparent;
            flex-direction: column;
            .text {
                text-align: center;
                font-size: 14px;
                width: 100%;
                font-weight: 600;
            }
        }
        .cb-sub-title {
            display: block;
            width: 100%;
        }
        .cb-checkbox {
            .checkbox {
                display: none;
                &:checked ~ .label {
                    .check-mark {
                        opacity: 1;
                    } 
                }
            }
            .check-mark {
                background-image: url("../assets/images/checkmark.png");
                background-size: 10px;
                background-position: center;
                background-repeat: no-repeat;
                display: block;
                width: 100%;
                height: 100%;
            } 
            .label {
                height: 18px;
                width: 18px;
                border: 2px solid $primaryText;
                display: flex;
                justify-content: center;
                align-items: center;
                cursor: pointer;
                .check-mark {
                    opacity: 0;
                    transition: all 0.2s ease-in-out;
                }
            }
        }
        .cb-filter-group {
            display: flex;
            align-items: center;
            padding-left: 15px;
            margin-right: 15px;
            @media screen and (max-width: 767px) {
                flex-wrap: wrap;
                .cb-filter, .show-entries, .cb-btn {
                    margin-bottom: 10px;
                    margin-right: 14px;
                }
            }
            .ml-auto {
                margin-left: auto;
                @media screen and (max-width: 767px) {
                    margin-left: 0;
                }
            }
            .cb-btn {
                margin-left: 25px;
                @media screen and (max-width: 767px) {
                    margin-left: 0;
                }
            }
            .show-entries {
                margin-right: 35px;
                display: flex;
                margin-left: 25px;
                align-items: center;
                @media screen and (max-width: 991px) {
                    margin-right: 15px;
                    margin-left: 15px;
                }
                input[type=number] {
                    color: $primaryText;
                    border: 0;
                    font-size: 18px;
                    width: 60%;
                    text-align: center;
                    background-color: transparent;
                    @media screen and (max-width: 991px) {
                        font-size: 14px;
                    }
                    &:focus {
                        outline: 0;
                        box-shadow: none;
                    }
                    &::-webkit-inner-spin-button { 
                        -webkit-appearance: none;
                     }
                    &::-webkit-outer-spin-button { 
                       -webkit-appearance: none;
                    }
                }
                .entries-count {
                    display: flex;
                    background-color: $gray;
                    max-width: 82px;
                    border-radius: 8px;
                    height: 58px;
                    @media screen and (max-width: 991px) {
                        height: 38px;
                    }
                }
                .entries-btns {
                    display: flex;
                    flex-direction: column;
                    justify-content: center;
                    button {
                        border: 0;
                        max-width: 11px;
                        padding: 0;
                        width: 15px;
                        height: 15px;
                        background-color: transparent;
                        img {
                            width: 100%;
                        }
                        &.up-btn {
                        background-image: url("../assets/images/up-arrow-icon.png");
                        background-repeat: no-repeat;
                        background-size: 15px;
                        background-position: center;
                        }
                        &.down-btn {
                        background-image: url("../assets/images/down_arrow.png");
                        background-repeat: no-repeat;
                        background-size: 15px;
                        background-position: center;
                        }
                    }
                    
                }
                .label {
                    font-size: 18px;
                    font-weight: 500;
                    color: $primaryText;
                    margin: 0 5px;
                    @media screen and (max-width: 991px) {
                        font-size: 14px;
                    }
                }
            }
        }
        .cb-filter_btn {
            &.bg-gray {
                border-color: $gray;
            }
        }
        .table-responsive {
            overflow-x: auto;
            &::-webkit-scrollbar-track {
                border-radius: 2;
                background-color: #1b2133;
            }
        
            &::-webkit-scrollbar {
                height: 1px;
                background-color: #ddd;
            }
        
            &::-webkit-scrollbar-thumb {
                border-radius: 2px;
                background-color: #1b2133;
            }
        }
        .table {
            border-spacing: 0;
            width: 100%;
            margin-top: 20px;
            min-width: 1400px;
            thead {
                background-color: #b5ddf1;
            }
            td, th {
                padding: 1vw 0;
                font-size: 0.6vw;
                color: $primaryText;
                font-weight: 500;
                @media screen and (max-width: 1599px) {
                    font-size: 13px;
                    padding: 20px 0;
                }
                &:first-child {
                    padding-left: 15px;
                }
                &.conditional {
                    font-weight: 600;
                    font-size: 14px;
                }
            }
        }
        .cb-pagination {
            padding-top: 40px;
            padding-bottom: 60px;
            padding-left: 100px;
            display: flex;
            @media screen and (max-width: 767px) {
                padding-left: 20px;
            }
        }

    }
    .cb-pagination {
        .pagination {
            display: inline-flex;
        }
        .item {
            margin: 0 4px;
            height: 40px;
            width: 40px;
            border-radius: 12px;
            overflow: hidden;
            font-size: 18px;
            color: $primaryText;
            display: flex;
            justify-content: center;
            align-items: center;
            @media screen and (max-width: 1599px) {
                height: 32px;
                width: 32px;
                border-radius: 8px;
            }
            @media screen and (max-width: 1279px) {
                height: 26px;
                width: 26px;
                img {
                    width: 14px;
                }
            }
            @media screen and (max-width: 479px) {
                margin: 0 2px;
                height: 23px;
                width: 23px;
            }
            
            @media screen and (max-width: 1599px) {
                font-size: 16px;
            }
            @media screen and (max-width: 1279px) {
                font-size: 14px;
            }
            &.active {
                background-color: $lightBlue;
                color: #fff;
            }
            cursor: pointer;
            &.btn-nav {
                background-color: $gray;
                display: flex;
                justify-content: center;
                align-content: center;
            }
            .double{
              background-repeat: no-repeat;
              display: block;
              width: 17px;
              height: 17px;
              margin-bottom: 3px;
              &.left {
                background-image: url("../assets/images/pagination-arrow-iconLeft1.png");
                
              }
              &.right {
                background-image: url("../assets/images/pagination-arrow-iconRight1.png");
              }
            }
            .chevron {
              background-repeat: no-repeat;
              display: block;
              width: 17px;
              height: 17px;
              margin-bottom: 3px;
              &.left {
                background-image: url("../assets/images/pagination-arrow-iconLeft2.png");
                
              }
              &.right {
                background-image: url("../assets/images/pagination-arrow-iconRight2.png");
              }
            }
        }
    } 
</style>
