<template>
  <div>
    <el-table
      :data="currentPageData"
      border
      style="width: 100%"
      :header-cell-style="{ background: '#ff7f00', color: '#fff' }"
    >
      <el-table-column prop="id" label="ID" width="180"> </el-table-column>
      <el-table-column prop="category" label="主目录分类" width="180">
      </el-table-column>
      <el-table-column prop="website" label="购物网站排行" width="180">
      </el-table-column>
      <el-table-column prop="status" label="状态" width="180">
      </el-table-column>
      <el-table-column label="操作" width="220">
    <template #default="scope">
      <el-button 
        type="primary" 
        size="small"
        @click="handleEdit(scope.row)"
        style="margin-right: 10px"
      >
        编辑
      </el-button>
      <el-button 
        type="danger" 
        size="small"
        @click="handleDelete(scope.row)"
      >
        删除
      </el-button>
    </template>
  </el-table-column>
    </el-table>

    <div class="block">
      <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"
        :current-page="currentPage"
        :page-sizes="[2, 4, 6, 8]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="tableData.length"
      >
      </el-pagination>
    </div>
     <el-button 
      type="primary" 
      class="fixed-add-btn"
      @click="handleAdd"
    >
      <i class="el-icon-plus"></i> 新增
    </el-button>
    <PopupComponent
    :visible.sync="dialogVisible"
      :form-data="currentForm"
      :is-edit="isEditMode"
      @submit="handleSubmit"
      @cancel="handleCancel"/>
  </div>
</template>

<script>

import PopupComponent from './PopupComponent.vue';
 
export default {
  name: "FormComponents",
  components: {
    PopupComponent
  },
  data() {
    return {
      currentPage: 1,
      pageSize: 2,
      tableData: [
        { id: 1, category: "电子产品", website: 1, status: "启用" },
        { id: 2, category: "服装服饰", website: 2, status: "停用" },
        { id: 3, category: "图书音像", website: 3, status: "启用" },
        { id: 4, category: "家居用品", website: 4, status: "停用" },
        { id: 5, category: "美妆个护", website: 5, status: "启用" },
        { id: 6, category: "食品生鲜", website: 6, status: "停用" },
      ],
      dialogVisible: false,
      isEditMode: false,
      currentForm: this.getEmptyForm(),
    };
  },
  computed: {
    currentPageData() {
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.tableData.slice(start, end);
    },
  },
  methods: {
 
    getEmptyForm() {
      return {
        id: null,
        categoryZh: '',
        categoryEn: '',
        sort: 1,
        status: '启用'
      };
    },
 
    handleSizeChange(val) {
      this.pageSize = val;
    },
    handleCurrentChange(val) {
      this.currentPage = val;
    },
    handleEdit(row) {
      this.isEditMode = true;
      this.currentForm = JSON.parse(JSON.stringify(row));
      this.dialogVisible = true;
    },
    handleDelete(row) {
      this.$confirm('确认删除该记录吗？', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning'
      }).then(() => {
        const index = this.tableData.findIndex(item => item.id === row.id);
        if (index !== -1) {
          this.tableData.splice(index, 1);
          if (this.currentPageData.length === 0 && this.currentPage > 1) {
            this.currentPage -= 1;
          }
        }
        this.$message.success('删除成功!');
      }).catch(() => {
        this.$message.info('已取消删除');
      });
    },
    handleSubmit(formData) {
      
    if (this.isEditMode) {
    const index = this.tableData.findIndex(item => item.id === formData.id);
    this.tableData.splice(index, 1, formData);
  } else {
    // 生成新ID（当前最大ID+1）
    const maxId = Math.max(...this.tableData.map(item => item.id), 0);
    formData.id = maxId + 1;
    
    
    this.tableData.unshift({
      ...formData,
      website: `${formData.ranking}`, 
      status: formData.status || '启用'
    });
    this.currentPage = 1;
  }
  this.dialogVisible = false;
    },
    handleAdd() {
      this.isEditMode = false;
      this.currentForm = this.getEmptyForm();
      this.dialogVisible = true;
    },
    handleCancel() {
      this.dialogVisible = false;
      this.$message.info('已取消操作');
    }
  }
};
</script>


<style scoped>

::v-deep .el-table th {
  background-color: #ff7f00 !important;
  color: white;
}


.block {
  margin-top: 20px;
  text-align: center;
}
.fixed-add-btn {
  position: fixed;
  right: 40px;
  bottom: 40px;
  z-index: 999;
  padding: 12px 20px;
  box-shadow: 0 2px 12px 0 rgba(0, 0, 0, 0.2);
}
 

.fixed-add-btn:hover {
  transform: translateY(-2px);
  transition: transform 0.3s;
}
</style>