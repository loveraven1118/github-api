<template>
    <div class="issue">
      <h1>Github Issue List</h1>
      <DataTable />
    </div>
</template>

<script>
import DataTable from '@/components/DataTable.vue'

export default {
  name: 'IssueView',
  components: {
    DataTable
  }
}
</script>
