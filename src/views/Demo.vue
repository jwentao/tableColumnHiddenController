<template>
  <div class="home">
    <div class="flex-wrap">
      <Setting
        :condition="tableCondition"
        @on-show="handleSettingShow"
        @on-save="handleSettingSave"
      ></Setting>
    </div>
    <el-table
      ref="table"
      :data="tableData"
      :checked="tableChecked"
      border
      @selection-change="handleSelectionChange"
    >
      <el-table-column
        type="selection"
        width="55"
        align="center"
        fixed
      />

      <el-table-column
        v-for="item in columns"
        :key="item.key"
        :label="item.label"
        align="center"
        :prop="item.key"/>

      <el-table-column
        label="操作"
        align="center"
      >
        <template>
          <el-button type="text">按钮</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import columnsCtrl from '../mixins/columnsCtrl'

export default {
  name: 'Home',
  mixins: [columnsCtrl],
  data: () => ({
    tableData: [],
    columns: []
  }),
  created () {
    // mock data
    const data = {}
    for (let i = 1; i <= 10; i++) {
      const key = `column${i}`
      this.columns.push({
        key,
        label: `label${i}`
      })
      data[key] = `${key}数据`
    }
    for (let i = 0; i < 9; i++) {
      this.tableData.push({ ...data })
    }
  },
  methods: {
    handleSelectionChange (val) {
      console.log(val)
    }
  }
}
</script>
<style scoped>
.flex-wrap {
  display: flex;
  justify-content: right;
}
</style>
