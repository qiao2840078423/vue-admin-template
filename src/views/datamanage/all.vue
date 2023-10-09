<template>
  <div class="dashboard-editor-container">
    <el-table :data="tableData" border style="width: 100%" max-height="1000">
      <el-table-column prop="id" align="center" label="代码"> </el-table-column>
      <el-table-column prop="name" label="名称"> </el-table-column>
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
const tableData = [
  {
    id: 1,
    name: "水电站1",
    locate: "空间维度1",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 2,
    name: "水电站2",
    locate: "空间维度2",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 3,
    name: "水电站3",
    locate: "空间维度3",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 4,
    name: "水电站4",
    locate: "空间维度4",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 5,
    name: "水电站5",
    locate: "空间维度5",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 6,
    name: "水电站6",
    locate: "空间维度6",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 7,
    name: "水电站7",
    locate: "空间维度7",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 8,
    name: "水电站8",
    locate: "空间维度8",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 9,
    name: "水电站9",
    locate: "空间维度9",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 10,
    name: "水电站10",
    locate: "空间维度10",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 11,
    name: "水电站11",
    locate: "空间维度11",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 12,
    name: "水电站12",
    locate: "空间维度12",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 1,
    name: "水文站1",
    locate: "空间维度1",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 2,
    name: "水文站2",
    locate: "空间维度2",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 3,
    name: "水文站3",
    locate: "空间维度3",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
  {
    id: 4,
    name: "水文站4",
    locate: "空间维度4",
    preDate: "2023-9-1",
    endDate: "2023-10-1",
  },
];

export default {
  name: "DataAll",
  data() {
    return {
      tableData: tableData,
    };
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
</style>