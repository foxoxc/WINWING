
<template>
  <el-dialog
    :visible.sync="localVisible"
    :title="isEdit ? '修改记录' : '新增记录'"
    width="600px"
    custom-class="custom-dialog"
  >
    <div class="dialog-header">
      <span class="dialog-title">{{ isEdit ? '修改' : '新增' }}</span>
      <i class="el-icon-close" @click="handleClose"></i>
    </div>

    <el-form
      ref="dataForm"
      :model="localFormData"
      :rules="rules"
      label-width="120px"
      class="form-container"
    >
 <el-form-item label="主目录分类名称" prop="category">
  <el-input 
    v-model="localFormData.category"
    maxlength="50"
    show-word-limit
    placeholder="请输入分类名称"
  />
</el-form-item>

      <el-form-item label="主目录分类名称（英文）" prop="categoryEn">
        <el-input
          v-model="localFormData.categoryEn"
          maxlength="50"
          show-word-limit
          placeholder="请输入英文名称"
        />
      </el-form-item>

<el-form-item label="网站排行" prop="ranking">
  <el-input-number 
    v-model="localFormData.ranking"
    :min="1"
    controls-position="right"
  />
</el-form-item>

      <el-form-item label="状态" prop="status">
        <el-radio-group v-model="localFormData.status">
          <el-radio label="启用">启用</el-radio>
          <el-radio label="停用">停用</el-radio>
        </el-radio-group>
      </el-form-item>
    </el-form>

    <div class="dialog-footer">
      <el-button @click="handleCancel">取消</el-button>
      <el-button type="primary" @click="handleSubmit">确认</el-button>
    </div>
  </el-dialog>
</template>

<script>
export default {
  name: 'PopupComponent',
  props: {
    visible: {
      type: Boolean,
      default: false
    },
    formData: {
      type: Object,
      default: () => ({
        id: null,
        categoryZh: '',
        categoryEn: '',
        sort: 1,
        status: '启用'
      })
    },
    isEdit: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      localFormData: {
       id: 1,
    category: "电子产品", 
    ranking: 1,         
    status: "启用"
      },
      rules: {
        categoryZh: [
          { required: true, message: '请输入中文名称', trigger: 'blur' },
          { max: 50, message: '长度不能超过50个字符', trigger: 'blur' }
        ],
        categoryEn: [
          { required: true, message: '请输入英文名称', trigger: 'blur' },
          { max: 50, message: '长度不能超过50个字符', trigger: 'blur' }
        ],
        sort: [
          { required: true, message: '请输入排序值', trigger: 'change' }
        ],
        status: [
          { required: true, message: '请选择状态', trigger: 'change' }
        ]
      }
    }
  },
  computed: {
    localVisible: {
      get() {
        return this.visible
      },
      set(val) {
        this.$emit('update:visible', val)
      }
    }
  },
  watch: {
    formData: {
      immediate: true,
      deep: true, // 添加深度监听
      handler(newVal) {
        this.localFormData = { ...newVal }
      }
    }
  },
  methods: {
    handleSubmit() {
      this.$refs.dataForm.validate(valid => {
        if (valid) {
          this.$emit('submit', { ...this.localFormData })
          this.resetForm()
          this.localVisible = false
        }
      })
    },
    handleCancel() {
      this.resetForm()
      this.localVisible = false
      this.$emit('cancel')
    },
    handleClose() {
      this.resetForm()
      this.localVisible = false
    },
    resetForm() {
      this.localFormData = {
        id: null,
        categoryZh: '',
        categoryEn: '',
        sort: 1,
        status: '启用'
      }
      this.$nextTick(() => {
        this.$refs.dataForm?.clearValidate()
      })
    }
  }
}
</script>

<style scoped>

.custom-dialog ::v-deep .el-dialog__header {
  display: none;
}

.dialog-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  border-bottom: 1px solid #ebeef5;
}

.dialog-title {
  font-size: 18px;
  font-weight: 600;
  color: #303133;
}

.el-icon-close {
  font-size: 20px;
  cursor: pointer;
  color: #909399;
}

.el-icon-close:hover {
  color: #409EFF;
}

.form-container {
  padding: 30px 20px;
}

.dialog-footer {
  text-align: center;
  padding: 20px 0;
}

.dialog-footer .el-button {
  width: 120px;
  margin: 0 15px;
}

.el-input-number {
  width: 120px;
}

.el-radio-group {
  line-height: 40px;
}
</style>