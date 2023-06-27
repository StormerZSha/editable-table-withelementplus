<template>
    <div class="editableTable">
        <div class="tableTop">
            <el-button  type="primary" >Add</el-button>
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
                <el-table-column fixed="right" label="Operations" width="120">
                    <template #default>
                      <el-button link type="primary" size="small">Edit</el-button>
                      <el-button link type="danger" size="small">Remove</el-button>
                    </template>
                </el-table-column>
            </el-table>
        </div>
    </div>
</template>
<script setup>
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