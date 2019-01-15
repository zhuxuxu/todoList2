<template>
  <el-row>
    <el-col :xs="24" :sm="18" :md="14" :lg="10" id="main">
    姓名：{{info.name}}
    <el-input v-model="info.name" placeholder="请输入姓名"></el-input>
    年龄：{{info.age}}
    <el-input v-model="info.age" placeholder="请输入年龄"></el-input>
    性别：{{info.sex}}
    <el-select v-model="info.sex" placeholder="请选择性别">
      <el-option v-for="item in options" :key="item" :value="item"></el-option>
    </el-select>
    <el-button @click="create" type="success">创建</el-button>
    <template>
      <el-table :data="tabledata" align="left">
        <el-table-column label="姓名" prop="name"></el-table-column>
        <el-table-column label="年龄" prop="age"></el-table-column>
        <el-table-column label="性别" prop="sex"></el-table-column>
        <el-table-column label="操作">
          <template slot-scope="a">
            <el-button type="danger" size="mini" @click="del(a.$index)">删除</el-button>
          </template>
        </el-table-column>
      </el-table>
    </template>
    </el-col>
  </el-row>
</template>
<script>
import Storage from '../store/store'
export default {
  name:"NewContact",
  data(){
    return{
      info:{
        name:'',
        age:'',
        sex:''
      },
      options:['男','女','保密'],
      tabledata:Storage.fetch()
    }
  },
  methods:{
    create(){
      this.tabledata.push(this.info)
      this.info={name:'',age:'',sex:''}
    },
    del(index){
      this.tabledata.splice(index,1)
    }
  },
  watch:{
    tabledata:{
      handler(items){Storage.save(items)},
      deep: true
    }
  }
}
</script>
<style>
   #main{float: none;margin: 0 auto;}
  .el-input{ padding-bottom: 5px;}
  .el-select {display: block;}
  .btn-auto{width: 100%;margin-top: 12px;}
</style>
