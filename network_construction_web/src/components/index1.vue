<style>
   .main1 {
     margin-top: 20px;
     margin-left: 50px;
   }
      .main2 {
     margin-top: 20px;
     margin-left: 50px;
   }
   .upload-demo {
      margin-bottom: 20px;
      margin-left: 50px;
   }
   .redirect {
     margin-top: 20px;
     margin-left: 390px;
   }
</style>

<template>
 <div class="left-navi">
  <el-row class="tac">
   <el-col :span="4">
     <el-menu
      default-active="2"
      class="el-menu-vertical-demo"
      @open="handleOpen"
      @close="handleClose">
      <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>导入数据</span>
        </template>
      </el-submenu>
      <el-submenu index="2">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>构建网络</span>
        </template>
      </el-submenu>
      <el-submenu index="3">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>社区划分</span>
        </template>
      </el-submenu>
      <el-submenu index="4">
        <template slot="title">
          <i class="el-icon-location"></i>
          <span>对比分析</span>
        </template>
      </el-submenu>
    </el-menu>
   </el-col>
   <el-col :span="10">
     <div class='main1'>
         <el-upload
            class="upload-demo"
            action=""
            :on-change="handleChange1"
            :file-list="fileListUpload1"
            accept=".csv"
            :auto-upload="false">
            <el-button size="small" type="primary">上传合著网络源文件</el-button>
         </el-upload>
         <el-table :data="tableData1" border style="width: 50%"
          :header-cell-style="{background:'#EEF6FD',color:'#251E25'}" slot="empty">
           <el-table-column prop="name" label="源节点ID" align="center"></el-table-column>
           <el-table-column prop="nameRemark" label="目标节点ID" align="center"></el-table-column>
         </el-table>
         <el-button type="primary" class='redirect' @click="gotonetwork">构建网络</el-button>
     </div>
    </el-col>
    <el-col :span="10">
     <div class='main2'>
         <el-upload
            class="upload-demo"
            action=""
            :on-change="handleChange2"
            :file-list="fileListUpload2"
            accept=".csv"
            :auto-upload="false">
            <el-button size="small" type="primary">上传贡献网络源文件</el-button>
         </el-upload>
         <el-table :data="tableData2" border style="width: 50%"
          :header-cell-style="{background:'#EEF6FD',color:'#251E25'}" slot="empty">
           <el-table-column prop="name" label="源节点ID" align="center"></el-table-column>
           <el-table-column prop="nameRemark" label="目标节点ID" align="center"></el-table-column>
         </el-table>
     </div>
    </el-col>
   </el-row>
 </div>


</template>

<script>
import Papa from 'vue-papa-parse'
  export default {
    data(){
     	return{
      	fileTemp: null,
        fileListUpload1: [],
        fileListUpload2: [],
        tableData1: [],
        tableData2: [],

     }
     },
    methods: {
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      handleChange1(file, fileList) {
       	this.fileTemp = file.raw
   	    if (this.fileTemp) {
      	  
          this.importcsv1(file.raw)
    	    
   	    } else {
    	     this.$message({
   			      type: 'warning',
              message: '请上传附件！'
            	})
  	      	}
      },
      importcsv1 (obj) {
        console.log('开始导入数据到表格')
        let _this = this//如果需要点击事件结束之后对DOM进行操作使用)_this.xx=xx进行操作
        this.$papa.parse(obj, {
          complete (results) {
            console.log(results)//csv文件的数据
            let data = []
            //遍历csv文件中的数据，存放到data中 方法不唯一，可自己更改
            for (let i = 0; i < 11; i++) {
              let obj = {}
              obj.name = results.data[i][0]
              obj.nameRemark = results.data[i][1]
              data.push(obj)
            }
            data.splice(0, 1)//将数组第一位的表格名称去除
            let num = 0
            console.log('data', data)
            _this.tableData1 = data//将数据放入要展示的表格中
          }
        })
      },
      handleChange2(file, fileList) {
       	this.fileTemp = file.raw
   	    if (this.fileTemp) {
      	  
          this.importcsv2(file.raw)
    	    
   	    } else {
    	     this.$message({
   			      type: 'warning',
              message: '请上传附件！'
            	})
  	      	}
      },
      importcsv2 (obj) {
        console.log('开始导入数据到表格')
        let _this = this//如果需要点击事件结束之后对DOM进行操作使用)_this.xx=xx进行操作
        this.$papa.parse(obj, {
          complete (results) {
            console.log(results)//这个是csv文件的数据
            let data = []
            //遍历csv文件中的数据，存放到data中 方法不唯一，可自己更改
            for (let i = 0; i < 11; i++) {
              let obj = {}
              obj.name = results.data[i][0]
              obj.nameRemark = results.data[i][1]
              data.push(obj)
            }
            data.splice(0, 1)//将数组第一位的表格名称去除
            let num = 0
            console.log('data', data)
            _this.tableData2 = data//将数据放入要展示的表格中
          }
        })
      },
      gotonetwork(){
        window.open("../../static/network.html")
      },
      
    }
  }
</script>