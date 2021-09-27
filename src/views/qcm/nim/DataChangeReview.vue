<template>
  <div class="app-container">
    <div class="head-container">
      <div>
        <el-form inline :model="queryModel">
          <el-form-item>
            <el-input v-model="queryModel.configName" placeholder="输入配置名称进行搜索" />
          </el-form-item>
          <el-form-item>
            <el-button class="filter-item" size="mini" type="success" icon="el-icon-search" @click="toQuery">搜索
            </el-button>
            <el-button
              class="filter-item"
              size="mini"
              type="warning"
              icon="el-icon-refresh-left"
              @click="resetQuery()"
            >
              重置
            </el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
    <!--    <el-dialog :visible.sync="dialogModel.visible" :title="dialogModel.title">-->
    <!--      <el-form :model="approveInfo">-->
    <!--        <el-form-item>-->
    <!--          <el-input v-model="approveInfo.type" disabled/>-->
    <!--        </el-form-item>-->
    <!--        <el-form-item>-->
    <!--          <el-input v-model="approveInfo.reason" placeholder="请输入申请原因"/>-->
    <!--        </el-form-item>-->
    <!--      </el-form>-->
    <!--      <div slot="footer">-->
    <!--        <el-button-->
    <!--          class="filter-item"-->
    <!--          size="mini"-->
    <!--          type="success"-->
    <!--          icon="el-icon-refresh-left"-->
    <!--          @click="resetQuery()"-->
    <!--        >-->
    <!--          提交-->
    <!--        </el-button>-->
    <!--        <el-button-->
    <!--          class="filter-item"-->
    <!--          size="mini"-->
    <!--          icon="el-icon-refresh-left"-->
    <!--          @click="dialogModel.visible = false"-->
    <!--        >-->
    <!--          取消-->
    <!--        </el-button>-->
    <!--      </div>-->
    <!--    </el-dialog>-->
    <!--    <el-dialog width="70%" :visible.sync="approvalListDialog.visible" :title="approvalListDialog.title">-->
    <!--      <el-table :data="approvalTableList">-->
    <!--        <el-table-column align="center" type="index" width="55"/>-->
    <!--        <el-table-column prop="type" label="申请类型"/>-->
    <!--        <el-table-column prop="time" label="申请时间"/>-->
    <!--        <el-table-column prop="reason" label="申请原因"/>-->
    <!--        <el-table-column prop="name" label="申请人"/>-->
    <!--        <el-table-column prop="status" label="申请状态"/>-->
    <!--        <el-table-column label="操作">-->
    <!--          <template slot-scope="props">-->
    <!--            <el-button-->
    <!--              size="mini"-->
    <!--              type="primary"-->
    <!--              :disabled="props.row['status'] !== '待审批'"-->
    <!--            >-->
    <!--              {{ '撤销申请' }}-->
    <!--            </el-button>-->
    <!--          </template>-->
    <!--        </el-table-column>-->
    <!--      </el-table>-->
    <!--    </el-dialog>-->
    <el-table :data="tableModel.tableData" style="width: 100%;">
      <el-table-column align="center" type="selection" width="55" />
      <el-table-column prop="type" label="申请类型" />
      <el-table-column prop="time" label="申请时间" />
      <el-table-column prop="reason" label="申请原因" />
      <el-table-column prop="name" label="申请人" />
      <el-table-column prop="status" label="申请状态" />
      <el-table-column label="操作" width="300">
        <template slot-scope="props">
          <el-button
            v-if="props.row['status'] === '待审批'"
            size="mini"
            type="primary"
          >
            {{ '审核通过' }}
          </el-button>
          <el-button
            v-if="props.row['status'] === '待审批'"
            size="mini"
            type="danger"
          >
            {{ '审核拒绝' }}
          </el-button>
        </template>
      </el-table-column>
    </el-table>
    <!--分页组件-->
    <el-pagination
      :page-size.sync="page.size"
      :total="page.total"
      :current-page.sync="page.page"
      style="margin-top: 8px;"
      layout="total, prev, pager, next, sizes"
      @size-change="sizeChangeHandler($event)"
      @current-change="pageChangeHandler"
    />
  </div>
</template>

<script>
export default {
  name: 'DataChangeReview',
  data() {
    return {
      queryModel: {
        configName: ''
      },
      page: {
        size: 10,
        total: 7,
        page: 1
      },
      tableModel: {
        tableData: [
          {
            type: '信息D',
            time: '2021-09-26 10:00:00',
            reason: '修改',
            name: 'xxx',
            status: '待审批'
          },
          {
            type: '信息D',
            time: '2021-08-26 09:00:00',
            reason: '新增',
            name: 'xxx',
            status: '已完结'
          },
          {
            type: '信息D',
            time: '2021-07-26 10:00:00',
            reason: '删除',
            name: 'xxx',
            status: '已完结'
          },
          {
            type: '信息B',
            time: '2021-08-26 09:00:00',
            reason: '修改',
            name: 'xxx',
            status: '已完结'
          },
          {
            type: '信息A',
            time: '2021-07-26 09:00:00',
            reason: '修改',
            name: 'xxx',
            status: '已完结'
          },
          {
            type: '信息E',
            time: '2021-06-26 09:00:00',
            reason: '修改',
            name: 'xxx',
            status: '已完结'
          },
          {
            type: '信息E',
            time: '2021-05-26 09:00:00',
            reason: '修改',
            name: 'xxx',
            status: '已完结'
          }
        ]
      },
      pop: false,
      dialogModel: {
        visible: false,
        title: '申请信息'
      },
      approveInfo: {
        type: '',
        reason: ''
      },
      approvalListDialog: {
        visible: false,
        title: '我的申请信息'
      },
      approvalTableList: [
        {
          type: '月度计划任务',
          time: '2021-09-26 10:00:00',
          reason: 'xxxx',
          name: 'xxx',
          status: '待审批'
        },
        {
          type: '月度计划任务',
          time: '2021-08-26 09:00:00',
          reason: 'xxxx',
          name: 'xxx',
          status: '已完结'
        },
        {
          type: '月度计划任务',
          time: '2021-07-26 09:00:00',
          reason: 'xxxx',
          name: 'xxx',
          status: '已完结'
        },
        {
          type: '月度计划任务',
          time: '2021-06-26 09:00:00',
          reason: 'xxxx',
          name: 'xxx',
          status: '已完结'
        },
        {
          type: '月度计划任务',
          time: '2021-05-26 09:00:00',
          reason: 'xxxx',
          name: 'xxx',
          status: '已完结'
        }
      ]
    }
  },
  methods: {
    toQuery() {
    },
    resetQuery() {
    },
    sizeChangeHandler() {
    },
    onPopoverShow() {
    },
    toEdit(row) {
      this.approveInfo.type = row.configName
      this.dialogModel.visible = true
    },
    pageChangeHandler() {
    },
    onPopoverHide() {
    },
    doCancel() {
    },
    doDelete() {
    },
    look() {
      this.approvalListDialog.visible = true
    }
  }
}
</script>

<style scoped>

</style>
