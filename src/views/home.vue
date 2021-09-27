<template>
  <div class="dashboard-container">
    <div class="dashboard-editor-container" style="background:#fff;">
      <!--      <panel-group @handleSetLineChartData="handleSetLineChartData"/>-->

      <el-row style="background:#fff;" :gutter="20">
        <el-col :span="12">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>代办任务 - 审批事务类</span>
              <el-button style="float: right; padding: 3px 0" type="text">未完成数量4</el-button>
            </div>
            <div v-for="o in 4" :key="o" class="text item">
              {{ '任务 ' + o }}
            </div>
          </el-card>
        </el-col>
        <el-col :span="12">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>代办任务 - 生产任务类</span>
              <el-button style="float: right; padding: 3px 0" type="text">未完成数量4</el-button>
            </div>
            <div v-for="o in 4" :key="o" class="text item">
              {{ '任务 ' + o }}
            </div>
          </el-card>
        </el-col>
      </el-row>

      <el-row style="background:#fff;margin-top: 16px" :gutter="20">
        <el-col :span="12">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>已办任务 - 审批事务类</span>
              <el-button style="float: right; padding: 3px 0" type="text">已完成数量4</el-button>
            </div>
            <div v-for="o in 4" :key="o" class="text item">
              {{ '任务 ' + o }}
            </div>
          </el-card>
        </el-col>
        <el-col :span="12">
          <el-card class="box-card">
            <div slot="header" class="clearfix">
              <span>已办任务 - 生产任务类</span>
              <el-button style="float: right; padding: 3px 0" type="text">已完成数量4</el-button>
            </div>
            <div v-for="o in 4" :key="o" class="text item">
              {{ '任务 ' + o }}
            </div>
          </el-card>
        </el-col>
      </el-row>

      <el-row style="background: #ffffff;margin-top: 16px" :gutter="20">
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="primary">串件申请</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="primary">换件申请</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="primary">补本申请</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="primary">续本、续页申请</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="primary">缺件申请</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="primary">修件申请</el-button>
        </el-col>
      </el-row>

      <el-row style="background: #ffffff;margin-top: 16px" :gutter="20">
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="info">任务管理</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="info">生产管理</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="info">质量管理</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="info">航材管理</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="info">部附件管理</el-button>
        </el-col>
        <el-col :span="4">
          <el-button style="margin: 0 auto" size="large" type="info">文件管理</el-button>
        </el-col>
      </el-row>
      <el-row :gutter="32">
        <el-col :xs="24" :sm="24" :lg="12">
          <div class="chart-wrapper">
            <radar-chart />
          </div>
        </el-col>
        <el-col :xs="24" :sm="24" :lg="12">
          <div class="chart-wrapper">
            <pie-chart />
          </div>
        </el-col>
        <!--        <el-col :xs="24" :sm="24" :lg="8">-->
        <!--          <div class="chart-wrapper">-->
        <!--            <bar-chart/>-->
        <!--          </div>-->
        <!--        </el-col>-->
      </el-row>
    </div>
  </div>
</template>

<script>
import PanelGroup from './dashboard/PanelGroup'
import LineChart from './dashboard/LineChart'
import RadarChart from '@/components/Echarts/RadarChart'
import PieChart from '@/components/Echarts/PieChart'

const lineChartData = {
  newVisitis: {
    expectedData: [100, 120, 161, 134, 105, 160, 165],
    actualData: [120, 82, 91, 154, 162, 140, 145]
  },
  messages: {
    expectedData: [200, 192, 120, 144, 160, 130, 140],
    actualData: [180, 160, 151, 106, 145, 150, 130]
  },
  purchases: {
    expectedData: [80, 100, 121, 104, 105, 90, 100],
    actualData: [120, 90, 100, 138, 142, 130, 130]
  },
  shoppings: {
    expectedData: [130, 140, 141, 142, 145, 150, 160],
    actualData: [120, 82, 91, 154, 162, 140, 130]
  }
}

export default {
  name: 'Dashboard',
  components: {
    // eslint-disable-next-line vue/no-unused-components
    PanelGroup,
    // eslint-disable-next-line vue/no-unused-components
    LineChart,
    RadarChart,
    PieChart
  },
  data() {
    return {
      lineChartData: lineChartData.newVisitis
    }
  },
  methods: {
    handleSetLineChartData(type) {
      this.lineChartData = lineChartData[type]
    }
  }
}
</script>

<style rel="stylesheet/scss" lang="scss" scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;

  .github-corner {
    position: absolute;
    top: 0;
    border: 0;
    right: 0;
  }

  .chart-wrapper {
    background: #fff;
    padding: 16px 16px 0;
    margin-bottom: 32px;
  }
}

@media (max-width: 1024px) {
  .chart-wrapper {
    padding: 8px;
  }
}
</style>
