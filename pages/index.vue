<template>
  <ag-grid-vue style="width: 1500px; height: 2000px" class="ag-theme-alpine" :defaultColDef="defaultColDef"
    :columnDefs="columnDefs" :rowData="rowData" rowSelection='multiple'>
  </ag-grid-vue>
</template>

<script lang="ts">
import Vue from 'vue';
import { AgGridVue } from 'ag-grid-vue';

export default Vue.extend({
  name: 'IndexPage',
  components: {
    AgGridVue
  },
  data() {
    return {
      columnDefs: null,
      rowData: null,
      defaultColDef: null,
    };
  },
  beforeMount() {
    this.defaultColDef = {
      width: 150,
      sortable: true,
      filter: true,
      resizable: true,
    };
    this.columnDefs = [
      { field: 'strDrink', headerName: 'Cocktail', checkboxSelection: true, },
      { field: 'strCategory', headerName: 'Category', },
      { field: 'strAlcoholic', headerName: 'Alcoholic', },
      { field: 'strGlass', headerName: 'Glass', },
      { field: 'strInstructions', headerName: 'Instructiones', flex: 1 },
    ];

    fetch('https://www.thecocktaildb.com/api/json/v1/1/search.php?f=m')
      .then(result => result.json())
      .then(rowData => this.rowData = rowData.drinks);
  },
})
</script>
