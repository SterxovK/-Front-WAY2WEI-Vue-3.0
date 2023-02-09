<template>
  <div class="table">
    <AgGridTable></AgGridTable>
  </div>
</template>

<script>
// @ is an alias to /src
import AgGridTable from '@/components/AgGridTable.vue'

export default {
  name: 'TableView',
  components: {
    AgGridTable
  }
}
</script>
