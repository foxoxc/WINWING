<!-- 搜索框 -->
<template>
  <div class="container">
    <div class="search_box">
      <p>搜索</p>
      <el-input
        v-model="searchValue"
        placeholder="请输入搜索内容"
        clearable
        @keyup.enter.native="handleSearch"
        class="search_input"
      >
        
      </el-input>
    </div>
    <!-- 状态栏 -->
    <div class="status_bar">
      <el-checkbox-group v-model="checkList">
        <div>
          <el-checkbox label="全选"></el-checkbox>
        </div>
        <div>
          <el-checkbox label="启用"></el-checkbox>
        </div>
        <div>
          <el-checkbox label="禁用"></el-checkbox>
        </div>
      </el-checkbox-group>
    </div>
    <!-- 按钮 -->
     <el-row class="screen">
      <el-button type="primary">确认筛选</el-button>
     </el-row>
     
  </div>

</template>

<script>

import { Button } from 'element-ui';

export default {
  name: "SearchBox",
  components:{
    'el-button': Button,
    
  },
  data() {
    return {
      checkList: ["选中且禁用", "复选框 A"],
    };
  },
};
</script>

<style>
.container {
  display: flex;
}
.search_box {
  display: flex;
  margin: 4vh;
}
.search_input {
  margin-left: 1vh;
}
.status_bar {
  display: flex;
  flex-direction: column;
   gap: 2vh;
   margin: 2vh;
}
.screen{
margin-left: auto;
}
.form_components{
display: flex;
}

</style>


