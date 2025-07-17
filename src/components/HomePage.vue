<template>
    <el-container>
  <el-header class="all_header" style="height: auto;">
    <!--name -->
   <div class="head_black">
     <p>WINWIN<span class="red-letter">G</span></p>
   </div>
   <!-- skip -->
     <div class="header-container">
   
    <div class="nav-group">
      <span class="nav-item">首页</span>
      <span class="nav-item">
         主目录分类♻ 
      </span>
    </div>
    <div class="back-text">返回</div>
  </div>

<div class="function_panel">
  <div class="line"></div>
  <div class="line_text"><p>功能面板</p></div>
  
</div>

  </el-header>
  <el-main>
    <SearchBox/>
    <div class="formComponents">
     <FormComponents/>
    </div>
      
  
  </el-main>
  
</el-container>

</template>
<script>
import FormComponents from './FormComponents.vue';

import SearchBox from './SearchBox.vue';

export default {
  name: 'HomePage',
 components:{
  SearchBox,
  FormComponents
 }

  
}
</script>
<style>
.head_black {
    background-color: black;  
    text-align: left;   
    
}
.head_black p {
    color: white;            
}
.red-letter {
    color: red;              
    
}
.head_black {
  display: flex;
  justify-content:first baseline; 
  align-items: center;    
  height: 8vh;
}
 
.head_black p {
  margin: 2vh;
  font-size: 7vh;    
 
}

.header-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2vh;
  height: 4vh;
  background: #DDDDDD;
  box-shadow: 0 2vh 4vh 0 rgba(0,0,0,0.1);
}
 
.nav-group {
  display: flex;
  align-items: center;
  gap: 30px;
}
 
.nav-item {
  color: #212223;
  font-size: 2vh;
  cursor: default;
  position: relative;
  padding-left: 18px;
}
 


 
.back-text {
  color: #1d1d1e;
  font-size: 14px;
  cursor: default;
}

/*  */
.function_panel{
  position: relative;
}
.line{
border: 0.1vh solid #909399bb;
position: absolute;
width: 100%;
margin:1.5vh 0 0 0;
z-index: -1;
}
.line_text{
  background-color: #fbfbfb;
  width: 10vh;
  height: auto;
  margin-left: 20px;
  font-size: 2vh;
  color: #909399;
  text-align: center;
}

</style>