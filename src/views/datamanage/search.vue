<template>
  <div class="dashboard-editor-container">
    <el-form :inline="true" :model="formInline">
      <el-form-item label="名称" class="form-inline">
        <el-input v-model="formInline.name" placeholder="请输入名称"></el-input>
      </el-form-item>
      <el-form-item class="form-inline">
        <el-button type="primary" size="small" @click="onSearch">搜 索</el-button>
      </el-form-item>
    </el-form>
    <el-table :data="tableData" border style="width: 100%" max-height="1000">
      <el-table-column prop="id" align="center" label="代码"> </el-table-column>
      <el-table-column prop="name" label="名称"> </el-table-column>
      <el-table-column prop="type" label="类型"> </el-table-column>
      <el-table-column prop="locate" label="空间维度"> </el-table-column>
      <el-table-column prop="preDate" label="生效时间"> </el-table-column>
      <el-table-column prop="endDate" label="失效时间"> </el-table-column>
      <el-table-column label="操作" align="center">
        <template slot-scope="scope">
          <router-link :to="`/detail/${scope.row.id}`">
            <el-button @click="handleClick(scope.row)" type="text" size="small"
              >详情</el-button
            >
          </router-link>
          <el-popconfirm title="确定删除吗？" @onConfirm="handleAdminDelete">
            <el-button
              slot="reference"
              type="text"
              size="small"
              class="myElButton"
              >删除</el-button
            >
          </el-popconfirm>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
const tableData = {
  shuidian: [
    {
      id: 1,
      name: "水电站1",
      type: '水电站',
      locate: "空间维度1",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 2,
      name: "水电站2",
      type: '水电站',
      locate: "空间维度2",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 3,
      name: "水电站3",
      type: '水电站',
      locate: "空间维度3",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 4,
      name: "水电站4",
      type: '水电站',
      locate: "空间维度4",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 5,
      name: "水电站5",
      type: '水电站',
      locate: "空间维度5",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 6,
      name: "水电站6",
      type: '水电站',
      locate: "空间维度6",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 7,
      name: "水电站7",
      type: '水电站',
      locate: "空间维度7",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 8,
      name: "水电站8",
      type: '水电站',
      locate: "空间维度8",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 9,
      name: "水电站9",
      type: '水电站',
      locate: "空间维度9",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 10,
      name: "水电站10",
      type: '水电站',
      locate: "空间维度10",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 11,
      name: "水电站11",
      type: '水电站',
      locate: "空间维度11",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 12,
      name: "水电站12",
      type: '水电站',
      locate: "空间维度12",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
  ],
  shuiwen: [
    {
      id: 1,
      name: "水文站1",
      type: '水文站',
      locate: "空间维度1",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 2,
      name: "水文站2",
      type: '水文站',
      locate: "空间维度2",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 3,
      name: "水文站3",
      type: '水文站',
      locate: "空间维度3",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
    {
      id: 4,
      name: "水文站4",
      type: '水文站',
      locate: "空间维度4",
      preDate: "2023-9-1",
      endDate: "2023-10-1",
    },
  ],
};

export default {
  name: "DataSearch",
  data() {
    return {
      tableData: null,
      type: null,
      formInline: {
        name: "",
      },
    };
  },
  mounted() {
    this.type = this.$route.params.type;
    this.tableData = tableData[this.type];
  },

  methods: {
    handleClick(row) {
      console.log(row);
    },
    handleAdminDelete() {
      this.$message({
        message: "删除成功！",
        type: "success",
      });
    },
    onSearch() {
      let name = this.formInline.name.trim()
      this.tableData = tableData[this.type].filter(obj => {
        return obj.name.includes(name)
      })
      this.$message({
        message: "搜索成功！",
        type: "success",
      });
    }
  },
};
</script>

<style scoped>
.dashboard-editor-container {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;
}

.myElButton {
  margin: 0 20px;
}

.form-inline {
  margin: 0 30px 20px 0;
}
</style>