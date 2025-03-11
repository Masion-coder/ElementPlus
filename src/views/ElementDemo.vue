<script setup>
import { ref } from "vue";
const tableData = [
    {
        date: "2016-05-03",
        name: "Tom",
        address: "No. 189, Grove St, Los Angeles",
    },
    {
        date: "2016-05-02",
        name: "Tom",
        address: "No. 189, Grove St, Los Angeles",
    },
    {
        date: "2016-05-04",
        name: "Tom",
        address: "No. 189, Grove St, Los Angeles",
    },
    {
        date: "2016-05-01",
        name: "Tom",
        address: "No. 189, Grove St, Los Angeles",
    },
];

const currentPage = ref(1);
const pageSize = ref(10);
const total = ref(40);
const size = ref("default");
const background = ref(true); // 是否显示背景色
const dialogTableVisible = ref(false);

const handleSizeChange = (val) => {
    console.log(`${val} items per page`);
};
const handleCurrentChange = (val) => {
    console.log(`current page: ${val}`);
};

// 表单组件
const user = ref({
    name: "",
    gender: "",
    birthday: "",
});

const onSubmit = () => {
    console.log(user.value);
};
</script>

<template>
    <div class="mb-4">
        <el-button>Default</el-button>
        <el-button type="primary">Primary</el-button>
        <el-button type="success">Success</el-button>
        <el-button type="info">Info</el-button>
        <el-button type="warning">Warning</el-button>
        <el-button type="danger">Danger</el-button>
    </div>

    <div class="mb-4">
        <el-button plain>Plain</el-button>
        <el-button type="primary" plain>Primary</el-button>
        <el-button type="success" plain>Success</el-button>
        <el-button type="info" plain>Info</el-button>
        <el-button type="warning" plain>Warning</el-button>
        <el-button type="danger" plain>Danger</el-button>
    </div>

    <!-- 表格 -->
    <div class="mb-4">
        <el-table :data="tableData" stripe style="width: 100%">
            <el-table-column prop="date" label="生日" width="180" align="center" />
            <el-table-column prop="name" label="Name" width="180" />
            <el-table-column prop="address" label="Address" />
        </el-table>
    </div>

    <!-- //分页条 -->
    <el-pagination
        class="mb-4"
        v-model:current-page="currentPage"
        v-model:page-size="pageSize"
        :page-sizes="[10, 20, 30, 40]"
        :size="size"
        :background="background"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total"
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange" />

    <!-- 对话框 -->
    <div class="mb-4">
        <el-button plain @click="dialogTableVisible = true"> 打开对话框 </el-button>
        <el-dialog v-model="dialogTableVisible" title="收货地址" width="800">
            <el-table :data="tableData">
                <el-table-column property="date" label="日期" width="150" />
                <el-table-column property="name" label="Name" width="200" />
                <el-table-column property="address" label="Address" /> </el-table
        ></el-dialog>
    </div>

    <!-- 表单组件 -->
    <div class="mb-4">
        <el-form :inline="true" :model="user" class="demo-form-inline">
            <el-form-item label="姓名">
                <el-input v-model="user.name" placeholder="请输入姓名" clearable />
            </el-form-item>
            <el-form-item label="性别">
                <el-select v-model="user.gender" placeholder="请选择" clearable>
                    <el-option label="男" value="1" />
                    <el-option label="女" value="2" />
                </el-select>
            </el-form-item>
            <el-form-item label="生日">
                <el-date-picker v-model="user.birthday" type="date" placeholder="请输入生日" value-format="YYYY-MM-DD" clearable />
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="onSubmit">Query</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<style scoped>
.mb-4 {
    margin-bottom: 10px;
}

/* 表单组件 */
.demo-form-inline .el-input {
    --el-input-width: 220px;
}

.demo-form-inline .el-select {
    --el-select-width: 220px;
}
</style>
