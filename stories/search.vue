<template>
  <el-data-table
      v-bind="$data"
      :hasEdit="false"
      :hasNew="false"
      :hasDelete="false"
      :customQuery="customQuery"
      >
        <template slot="search">
          <el-tag>slot=search</el-tag>
          <el-rate v-model="customQuery.rate" style="display: inline-block"></el-rate>
        </template>

      </el-data-table>
</template>
<script>
import ElDataTable from '../src/el-data-table.vue'
import config from './config'
import ElTag from 'element-ui/lib/tag'
import ElRate from 'element-ui/lib/rate'

export default {
  components: {ElDataTable, ElTag, ElRate},
  data: function() {
    let searchForm = [
      {
        $type: 'input',
        $id: 'q',
        label: 'github用户名',
        width: '200px',
        $el: {placeholder: '1分钟只能调用10次'},
        rules: [{required: true, trigger: 'blur', len: 3}]
      }
    ]

    let cfg = JSON.parse(JSON.stringify(config))
    cfg.searchForm = searchForm
    cfg.url = 'https://api.github.com/search/users'

    cfg.customQuery = {rate: 0}

    return cfg
  }
}
</script>
