<template>
  <div class="app-container">
    <div class="head-container">
      <el-form inline :model="queryModel">
        <!--        <el-form-item>-->
        <!--          <el-select-->
        <!--            v-model="queryModel.type"-->
        <!--            clearable-->
        <!--            size="small"-->
        <!--            placeholder="报表类型"-->
        <!--            class="filter-item"-->
        <!--          >-->
        <!--            <el-option value="1" label="飞机出厂情况变动表" />-->
        <!--            <el-option value="2" label="出厂飞机周期统计表" />-->
        <!--            <el-option value="3" label="出厂飞机按阶段统计表" />-->
        <!--            <el-option value="4" label="进场飞机周期列表" />-->
        <!--            <el-option value="5" label="修理完成飞机信息报表" />-->
        <!--          </el-select>-->
        <!--        </el-form-item>-->
        <el-form-item>
          <el-button class="filter-item" size="mini" type="success" icon="el-icon-search">统计生成
          </el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
export default {
  name: 'PropertyStatistics',
  data() {
    return {
      queryModel: {
        type: ''
      }
    }
  }
}
</script>

<style scoped>

</style>
