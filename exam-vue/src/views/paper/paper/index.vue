<template>

  <data-table
    ref="pagingTable"
    :options="options"
    :list-query="listQuery"
  >
    <template slot="filter-content">

      <el-input v-model="listQuery.params.title" placeholder="搜索规则名称" style="width: 200px;" class="filter-item" />

    </template>

    <template slot="data-columns">

      <el-table-column
        label="考试名称"
        align="center"
        prop="title"
      >

        <template slot-scope="scope">
          <router-link :to="{ name: 'ShowExam', params: {id : scope.row.id}}">
            {{ scope.row.title }}
          </router-link>

        </template>

      </el-table-column>

      <el-table-column
        label="考生姓名"
        align="center"
        prop="realName"
      />

      <el-table-column
        label="考试时间"
        align="center"
        prop="createTime"
      />

      <el-table-column
        label="考试时长(分钟)"
        align="center"
        prop="totalTime"
      >

        <template slot-scope="scope">
          {{ scope.row.userTime }} / {{ scope.row.totalTime }}
        </template>

      </el-table-column>

      <el-table-column
        label="客观分"
        align="center"
        prop="subjScore"
      />

      <el-table-column
        label="主观分"
        align="center"
        prop="objScore"
      />

      <el-table-column
        label="总分"
        align="center"
        prop="userScore"
      />

      <el-table-column
        label="考试状态"
        align="center"
      >

        <template slot-scope="scope">
          {{ scope.row.state | paperStateFilter }}
        </template>

      </el-table-column>

    </template>

  </data-table>

</template>

<script>
import DataTable from '@/components/DataTable'

export default {
  name: 'QuList',
  components: { DataTable },
  data() {
    return {

      listQuery: {
        current: 1,
        size: 10,
        params: {
          title: ''
        }
      },

      options: {

        // 可批量操作
        multi: false,
        // 列表请求URL
        listUrl: '/paper/paper/paging'
      }
    }
  },
  methods: {

  }
}
</script>
