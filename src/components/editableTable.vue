<template>
    <div class="editableTable">
        <div class="tableTop">
            <el-button type="primary" @click="addData">Add</el-button>
        </div>
        <div class="tableContainer">
            <el-table
                ref="table"
                :key="tableKey"
                :data="tableData"
                border
                fit
            >
                <el-table-column prop="name" label="Name" width="120" />
                <el-table-column prop="state" label="State" width="120" />
                <el-table-column prop="city" label="City" width="120" />
                <el-table-column prop="address" label="Address" width="600" />
                <el-table-column prop="zip" label="Zip" width="120" />
                <el-table-column fixed="right" label="Operations" width="150">
                    <template #default="scope">
                      <el-button link type="primary" size="small" v-show="editingIndex!=scope.$index" @click="editData(scope.$index)">Edit</el-button>
                      <el-button link type="danger" size="small"  v-show="editingIndex!=scope.$index" @click="removeData(scope.$index)">Remove</el-button>
                      <el-button link type="primary" size="small" v-show="editingIndex==scope.$index" @click="editDataConfirm(scope.$index)">Finish</el-button>
                      <el-button link type="danger" size="small"  v-show="editingIndex==scope.$index" @click="editDataCancle(scope.$index)">Cancle</el-button>
                    </template>
                </el-table-column>
            </el-table>
        </div>
    </div>
</template>
<script setup>
import 'element-plus/es/components/message/style/css'
import { ElMessage } from 'element-plus';
import {ref} from 'vue'

let tableData=ref([
   {
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
  },
  {
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
  },
  {
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
  },
  {
    name: 'Tom',
    state: 'California',
    city: 'Los Angeles',
    address: 'No. 189, Grove St, Los Angeles',
    zip: 'CA 90036',
  }   
])
let tableKey=ref(0)
let editingIndex=ref(null)
let table=ref()
let oldrowDatalist=ref([])

const addData=()=>{
    if (editingIndex.value!=null) {
        ElMessage.warning('please finish editing ! ')
        return;
    }
    tableData.value.push({
        name: 'Tom',
        state: 'California',
        city: 'Los Angeles',
        address: 'No. 189, Grove St, Los Angeles',
        zip: 'CA 90036',
    })
    tableKey.value++
}
const removeData=(index)=>{
    if (editingIndex.value!=null) {
        ElMessage.warning('please finish editing ! ')
        return;
    }
    tableData.value.splice(index,1)
    tableKey.value++
}
const editData=(index)=>{
    if (editingIndex.value!=null) {
        ElMessage.warning('please finish other editing ! ')
        return;
    }
    editingIndex.value=index
    let rowlist=table.value.$el.getElementsByClassName('el-table__row')
    let tdlist=rowlist[index].children
    oldrowDatalist.value=[]
    for(let i=0;i<tdlist.length-1;i++){
        let oldrowData=tdlist[i].innerText
        oldrowDatalist.value.push(oldrowData)
        tdlist[i].innerHTML=`
            <div class="cell">
                <div class="el-input">
                    <input type="text" placeholder="please input" class="el-input__inner" style="width:100%"/>    
                </div>
            </div>
        `
        let inputdom=tdlist[i].children[0].children[0].children[0]
        inputdom.value=oldrowData
    }
}
const editDataConfirm=(index)=>{
    editingIndex.value=null
    let obj= {
        name: '',
        state: '',
        city: '',
        address: '',
        zip: '',
    }
    let rowlist=table.value.$el.getElementsByClassName('el-table__row')
    let tdlist=rowlist[index].children
    for(let i=0;i<tdlist.length-1;i++){
        let inputdom = tdlist[i].children[0].children[0].children[0]
        tdlist[i].innerHTML=`
            <div class='cell'>
              ${inputdom.value}
            </div>`
        switch (i) {
            case 0:
                obj.name=inputdom.value
            break;
            case 1:
                obj.state=inputdom.value
            break;
            case 2:
                obj.city=inputdom.value
            break;
            case 3:
                obj.address=inputdom.value
            break;
            case 4:
                obj.zip=inputdom.value
            break;
            default:
            break;
        }
    }
    for(let i in obj){
        tableData.value[index][i]=obj[i]
    }
}
const editDataCancle=(index)=>{
    editingIndex.value=null
    let rowlist=table.value.$el.getElementsByClassName('el-table__row')
    let tdlist=rowlist[index].children
    for(let i=0;i<tdlist.length-1;i++){
        let inputdom = tdlist[i].children[0].children[0].children[0]
        tdlist[i].innerHTML=`
            <div class='cell'>
              ${oldrowDatalist.value[i]}
            </div>`
    }
}
</script>
<style lang="scss">
.editableTable{
    .tableTop{
        width: 100%;
        margin-bottom: 5px;
        display: flex;
        justify-content: flex-end;
    }
}
</style>