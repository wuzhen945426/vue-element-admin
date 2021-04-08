<template>
  <div class="components-container">
    <el-button type="primary" @click="dialogTableVisible = true">
      打开表格弹出框
    </el-button>
    <el-dialog v-el-drag-dialog :visible.sync="dialogTableVisible" title="Shipping address">
      <line-chart :chart-data="lineChartData" />
    </el-dialog>
  </div>
</template>

<script>
import elDragDialog from '@/directive/el-drag-dialog' // base on element-ui
import LineChart from '@/views/dashboard/admin/components/LineChart'


const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  }
}
export default {
  name: 'DragDialogDemo',
    components: {LineChart},
  directives: { elDragDialog },
  data() {
    return {
      dialogTableVisible: false,
     lineChartData: lineChartData.newVisitis
    }
  },
  methods: {

  }
}
</script>
