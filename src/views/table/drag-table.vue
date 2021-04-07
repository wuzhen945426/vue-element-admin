<template>
  <div class="app-container">
    <!-- Note that row-key is necessary to get a correct row order. -->
    <el-input v-model="inputed" placeholder="搜索" style="width:200px"></el-input>
    <el-table ref="dragTable" v-loading="listLoading" :data="list" row-key="id" border fit highlight-current-row style="width: 100%">
      <el-table-column align="center" label="ID" width="65">
        <template slot-scope="{row}">
          <span>{{ row.id }}</span>
        </template>
      </el-table-column>

      <el-table-column width="180px" align="center" label="Date">
        <template slot-scope="{row}">
          <span>{{ $moment(row.timestamp).format("YYYY-DD-MM")}}</span>
        </template>
      </el-table-column>

      <el-table-column min-width="300px" label="Title" prop="title"></el-table-column>

      <el-table-column width="110px" align="center" label="Author" prop="author"></el-table-column>

      <el-table-column width="100px" label="Importance" >
        <template slot-scope="{row}">
          <svg-icon v-for="n in + row.importance" :key="n" icon-class="star" class="icon-star"></svg-icon>
        </template>
      </el-table-column>

      <el-table-column align="center" label="Readings" width="95">
        <template slot-scope="{row}">
          <span>{{ row.pageviews }}</span>
        </template>
      </el-table-column>

      <el-table-column class-name="status-col" label="Status" width="110">
        <template slot-scope="{row}">
          <el-tag :type="row.status | statusFilter">
            {{ row.status }}
          </el-tag>
        </template>
      </el-table-column>

      <el-table-column align="center" label="Drag" width="80">
        <template slot-scope="{}">
          <svg-icon class="drag-handler" icon-class="drag" />
        </template>
      </el-table-column>
    </el-table>
    <pagination :total="total" :page.sync="listQuery.page" :limit.sync="listQuery.limit" @pagination="getList"></pagination>

  </div>
</template>

<script>
import { fetchList } from '@/api/article'
import Pagination from '@/components/Pagination' 

export default {
  name: 'DragTable',
  components: { Pagination },
  filters: {
    statusFilter(status) {
      const statusMap = {
        published: 'success',
        draft: 'info',
        deleted: 'danger'
      }
      return statusMap[status]
    }
  },
  data() {
    return {
      list: [],
      total: 0,
      listLoading: true,
      listQuery: {
        page: 1,
        limit: 10
      },
      inputed:'',
      deep:[]
    }
  },
  watch:{
    inputed(val) {
      this.deep = this.list
      if (!val) return this.getList();
      this.list = this.deep.filter(item => {
        return item.title.indexOf(val) !== -1;
      })
    }
  },
  created() {
    this.getList()
  },
  methods: {
    async getList() {
      this.inputed = ""   //每次点击分页或者其他方式调用接口清空输入框
      this.listLoading = true
      const { data } = await fetchList(this.listQuery)
      this.list = data.items
      this.total = data.total
      this.listLoading = false
    }
  }
}
</script>

<style>
.sortable-ghost{
  opacity: .8;
  color: #fff!important;
  background: #42b983!important;
}
</style>

<style scoped>
.icon-star{
  margin-right:2px;
}
.drag-handler{
  width: 20px;
  height: 20px;
  cursor: pointer;
}
.show-d{
  margin-top: 15px;
}
</style>
