<template>
  <div class="app-container">
    <!--工具栏-->
    <div class="head-container">
      <div>
        <!-- 搜索 -->
        <el-input clearable size="small" placeholder="模糊搜索" style="width: 200px;" class="filter-item" />
        <date-range-picker class="date-item" />
        <rrOperation />
      </div>
      <crudOperation :permission="permission" />
    </div>
  </div>
</template>

<script>
export default {
  name: 'MaintenanceProject'
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
::v-deep .el-input-number .el-input__inner {
  text-align: left;
}
::v-deep .vue-treeselect__control,::v-deep .vue-treeselect__placeholder,::v-deep .vue-treeselect__single-value {
  height: 30px;
  line-height: 30px;
}
</style>

