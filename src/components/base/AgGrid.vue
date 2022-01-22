<template>
  <ag-grid-vue
    class="ag-theme-material grid-class"
    :columnDefs="columnDefs"
    :rowData="rowData"
    :defaultColDef="defaultColDef"
  ></ag-grid-vue>
</template>

<script>
import { AgGridVue } from "ag-grid-vue";

export default {
  name: "AgGrid",
  components: {
    AgGridVue,
  },
  props: {
    columnDefs: {
      type: Array,
      required: true,
    },
    rowData: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      // setting default parameteres for grid for adding sortable,filter,
      // autowidth & header custom styles here.
      defaultColDef: {
        resizable: true,
        sortable: true,
        filter: true,
        headerClass: "header-grid-class",
        floatingFilter: true,
        flex: 1,
        minWidth: 150,
      },
    };
  },
};
</script>
<style >
.header-grid-class {
  background: radial-gradient(#f7dee1	, transparent) !important;
  color: #363472;
  font-family: Roboto;
  font-size: 14px ;
}
.grid-class{
  height: calc(100vh - 48px);
  margin:20px;
}
</style>