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
          @click="dialog = true"
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
    <el-dialog :visible.sync="dialog" :title="'上传图片'">
      <el-upload
        class="upload-demo"
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        :file-list="fileList"
        list-type="picture"
      >
        <el-button size="small" type="primary">点击上传</el-button>
        <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
      </el-upload>
    </el-dialog>
    <el-table :data="tableModel.tableData" style="width: 100%;">
      <el-table-column align="center" type="selection" width="55" />
      <el-table-column prop="configName" label="图片名称" />
      <el-table-column prop="isActive" label="图片内容">
        <template slot-scope="props">
          <el-image
            style="width: 100px; height: 100px"
            :src="props.row.isActive"
            :fit="'fill'"
          />
        </template>
      </el-table-column>
      <el-table-column prop="addUser" label="添加人" />
      <el-table-column prop="addTime" label="添加时间" />
      <el-table-column>
        <template slot-scope="props">
          <el-button
            size="mini"
            type="primary"
            icon="el-icon-edit"
            @click="toEdit(props.row)"
          />
          <el-popover
            v-model="pop"
            placement="top"
            width="180"
            trigger="manual"
            @show="onPopoverShow"
            @hide="onPopoverHide"
          >
            <p>{{ msg }}</p>
            <div style="text-align: right; margin: 0">
              <el-button size="mini" type="text" @click="doCancel">取消</el-button>
              <el-button
                type="primary"
                size="mini"
                @click="doDelete(props.row)"
              >确定
              </el-button>
            </div>
            <el-button
              slot="reference"
              type="danger"
              icon="el-icon-delete"
              size="mini"
            />
          </el-popover>
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
  name: 'DrawingFile',
  data() {
    return {
      queryModel: {
        configName: ''
      },
      fileList: [{ name: 'food.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100' }, { name: 'food2.jpeg', url: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100' }],
      page: {
        size: 10,
        total: 5,
        page: 1
      },
      tableModel: {
        tableData: [
          {
            configName: 'A',
            addUser: 'xxx',
            isActive: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
            addTime: '2021-09-27 14:16:00'
          },
          {
            configName: 'B',
            addUser: 'xxx',
            isActive: 'https://fuss10.elemecdn.com/e/5d/4a731a90594a4af544c0c25941171jpeg.jpeg',
            addTime: '2021-09-27 14:16:00'
          },
          {
            configName: 'C',
            addUser: 'xxx',
            isActive: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
            addTime: '2021-09-27 14:16:00'
          },
          {
            configName: 'D',
            addUser: 'xxx',
            isActive: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
            addTime: '2021-09-27 14:16:00'
          },
          {
            configName: 'E',
            addUser: 'xxx',
            isActive: 'https://fuss10.elemecdn.com/3/63/4e7f3a15429bfda99bce42a18cdd1jpeg.jpeg?imageMogr2/thumbnail/360x360/format/webp/quality/100',
            addTime: '2021-09-27 14:16:00'
          }
        ]
      },
      pop: false,
      dialog: false
    }
  },
  methods: {
    handleRemove(file, fileList) {
      console.log(file, fileList)
    },
    handlePreview(file) {
      console.log(file)
    },
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
