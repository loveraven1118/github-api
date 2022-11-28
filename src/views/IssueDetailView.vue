<template>
    <div class="issuedetail">
      <h1>Github Issue Detail</h1>
      <DataTable />
    </div>
</template>

<script>
import DataTable from '@/components/DataDetailTable.vue'

export default {
  name: 'IssueDetailView',
  components: {
    DataTable
  }
}
</script>
