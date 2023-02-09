<template>
  <button @click="deselectRows">deselect rows</button>
  <ag-grid-vue
    class="ag-theme-alpine"
    style="height: 500px"
    :columnDefs="columnDefs.value"
    :rowData="rowData.value"
    :defaultColDef="defaultColDef"
    rowSelection="multiple"
    animateRows="true"
    @cell-clicked="cellWasClicked"
    @grid-ready="onGridReady"
  >
  </ag-grid-vue>
</template>

<script>
import { AgGridVue } from 'ag-grid-vue3' // the AG Grid Vue Component
import { reactive, onMounted, ref } from 'vue'

import 'ag-grid-community/styles/ag-grid.css' // Core grid CSS, always needed
import 'ag-grid-community/styles/ag-theme-alpine.css' // Optional theme CSS

export default {
  name: 'AgGridTable',
  components: {
    AgGridVue
  },
  setup () {
    const gridApi = ref(null) // Optional - for accessing Grid's API

    // Obtain API from grid's onGridReady event
    const onGridReady = (params) => {
      gridApi.value = params.api
    }

    const rowData = reactive({}) // Set rowData to Array of Objects, one Object per Row

    // Each Column Definition results in one Column.
    const columnDefs = reactive({
      value: [
        {
          headerName: 'ФИО',
          colId: 'id',
          valueGetter: function (params) {
            if (params.data.questionnaire !== null) {
              return (
                params.data.questionnaire.last_name +
              ' ' +
              params.data.questionnaire.first_name +
              ' ' +
              params.data.questionnaire.patronymic
              )
            // eslint-disable-next-line no-empty
            } else {}
          }
        },
        { field: 'status', headerName: 'Статус' },
        { field: 'finished_at', headerName: 'Дата прохождения' },
        { field: 'report_type', headerName: 'Тип отчета' }
      ]
    })

    // DefaultColDef sets props common to all Columns
    const defaultColDef = {
      sortable: true,
      filter: true,
      flex: 1
    }

    // Example load data from sever
    onMounted(() => {
      fetch('https://ei-adult.way2wei.space/response.json')
        .then((result) => result.json())
        .then((remoteRowData) => (rowData.value = remoteRowData))
    })

    return {
      onGridReady,
      columnDefs,
      rowData,
      defaultColDef,
      cellWasClicked: (event) => {
        // Example of consuming Grid Event
        console.log('cell was clicked', event)
      },
      deselectRows: () => {
        gridApi.value.deselectAll()
      }
    }
  }
}
</script>

<style lang="scss"></style>
