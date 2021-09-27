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
            >重置
            </el-button>
          </el-form-item>
        </el-form>
      </div>
      <div style="float: left">
        <el-button
          class="filter-item"
          size="mini"
          type="primary"
          icon="el-icon-plus"
        >
          新增
        </el-button>
        <el-button
          class="filter-item"
          size="mini"
          type="success"
          icon="el-icon-edit"
        >
          修改
        </el-button>
        <el-button
          slot="reference"
          class="filter-item"
          type="danger"
          icon="el-icon-delete"
          size="mini"
        >
          删除
        </el-button>
        <el-button
          class="filter-item"
          size="mini"
          type="warning"
          icon="el-icon-download"
        >导出</el-button>
      </div>
      <div style="float: right">
        <el-button-group class="crud-opts-right">
          <el-button
            size="mini"
            plain
            type="info"
            icon="el-icon-search"
            @click="toggleSearch()"
          />
          <el-button
            size="mini"
            icon="el-icon-refresh"
            @click="crud.refresh()"
          />
          <el-popover
            placement="bottom-end"
            width="150"
            trigger="click"
          >
            <el-button
              slot="reference"
              size="mini"
              icon="el-icon-s-grid"
            >
              <i
                class="fa fa-caret-down"
                aria-hidden="true"
              />
            </el-button>
            <el-checkbox
              v-model="allColumnsSelected"
              :indeterminate="allColumnsSelectedIndeterminate"
              @change="handleCheckAllChange"
            >
              全选
            </el-checkbox>
            <el-checkbox
              v-for="item in tableColumns"
              :key="item.property"
              v-model="item.visible"
              @change="handleCheckedTableColumnsChange(item)"
            >
              {{ item.label }}
            </el-checkbox>
          </el-popover>
        </el-button-group>
      </div>
    </div>
    <el-table :data="tableModel.tableData" style="width: 100%;">
      <el-table-column align="center" type="selection" width="55" />
      <el-table-column prop="nums" label="所属飞机型号" />
      <el-table-column prop="configName" label="部附件名称" />
      <el-table-column prop="price" label="登记人" />
      <el-table-column prop="isActive" label="当前状态" />
      <el-table-column prop="addTime" label="登记日期" />
      <el-table-column>
        <template slot-scope="">
          <el-button
            size="mini"
            type="primary"
            icon="el-icon-edit"
          >分解登记</el-button>
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
  name: 'DecompositionBusinessManagement',
  data() {
    return {
      queryModel: {
        configName: ''
      },
      page: {
        size: 10,
        total: 3,
        page: 1
      },
      tableModel: {
        tableData: [
          {
            configName: 'xxx部附件1',
            nums: 'xxx飞机',
            price: 'xxx',
            isActive: '已登记',
            addTime: '2021-09-27 14:16:00'
          },
          {
            configName: 'xxx部附件2',
            nums: 'xxx飞机',
            price: 'xxx',
            isActive: '已登记',
            addTime: '2021-09-27 14:16:00'
          },
          {
            configName: 'xxx部附件3',
            nums: 'xxx飞机',
            price: 'xxx',
            isActive: '已登记',
            addTime: '2021-09-27 14:16:00'
          }
        ]
      },
      pop: false
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
    toEdit() {
    },
    pageChangeHandler() {
    },
    onPopoverHide() {
    },
    doCancel() {
    },
    doDelete() {
    }
  }
}
</script>

<style scoped>

</style>
