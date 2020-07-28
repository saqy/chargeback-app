<template>
  <div id="app" class="ui container">
    <input v-model="perPage" type="number" />
    <template>
      <select v-model="selectedCategory">
        <option
          v-for="option in columns"
          v-bind:value="option.name"
          :key="option.name"
        >{{ option.name }}</option>
      </select>
    </template>

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
    <div style="padding-top:10px">
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

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 20px;
}
button.ui.button {
  padding: 8px 3px 8px 10px;
  margin-top: 1px;
  margin-bottom: 1px;
}
</style>
