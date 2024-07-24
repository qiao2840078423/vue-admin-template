<template>
  <div class="detail">
    <el-button type="primary" @click="handleBack">返回</el-button>

    <!-- 基础信息表格 -->
    <!-- 标识信息 -->
    <h3>标识信息</h3>
    <el-table :data="idTableData" border :cell-class-name="cellClass">
      <el-table-column
        v-for="column in idTableColumns"
        :key="column.prop"
        :prop="column.prop"
        :label="column.label"
        align="center"
      >
      </el-table-column>
    </el-table>

    <!-- 特征信息 -->
    <h3>特征信息</h3>
    <el-table :data="feaTableData" border :cell-class-name="cellClass">
      <el-table-column
        v-for="column in feaTableColumns"
        :key="column.prop"
        :prop="column.prop"
        align="center"
        :label="column.label"
      >
      </el-table-column>
    </el-table>

    <!-- 时间信息 -->
    <h3>时间信息</h3>
    <el-table :data="dateTableData" border :cell-class-name="cellClass">
      <el-table-column
        v-for="column in dateTableColumns"
        :key="column.prop"
        :prop="column.prop"
        align="center"
        :label="column.label"
      >
      </el-table-column>
    </el-table>

    <!-- 时序数据 -->
    <h3>时序数据</h3>
    <el-row style="background: #fff; padding: 16px 16px 0; margin-bottom: 32px">
      <line-chart />
    </el-row>

    <div class="routerLink">
      <el-popconfirm title="确定删除吗?" @onConfirm="handleConfirm">
        <el-button slot="reference" type="danger">删 除</el-button>
      </el-popconfirm>
      <el-button
        type="success"
        class="myRouter"
        @click="dialogFormVisible = true"
        >编 辑</el-button
      >
    </div>

    <el-dialog :visible.sync="dialogFormVisible" top="7vh">
      <el-form :model="form">
        <el-form-item label="id" :label-width="formLabelWidth">
          <el-input v-model="form.id" autocomplete="off" disabled></el-input>
        </el-form-item>
        <el-form-item label="名 称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="空间维度" :label-width="formLabelWidth">
          <el-input v-model="form.locate" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="所属流域" :label-width="formLabelWidth">
          <el-input v-model="form.area" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="所属河流" :label-width="formLabelWidth">
          <el-input v-model="form.river" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="总库容" :label-width="formLabelWidth">
          <el-input v-model="form.totalStorage" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="调节库容" :label-width="formLabelWidth">
          <el-input v-model="form.adjustStorage" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="防洪库容" :label-width="formLabelWidth">
          <el-input v-model="form.floodStorage" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="业主单位" :label-width="formLabelWidth">
          <el-input v-model="form.unit" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="实控人" :label-width="formLabelWidth">
          <el-input v-model="form.controller" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="生效时间" :label-width="formLabelWidth">
          <el-input v-model="form.preDate" autocomplete="off" disabled></el-input>
        </el-form-item>
        <el-form-item label="失效时间" :label-width="formLabelWidth">
          <el-input v-model="form.endDate" autocomplete="off" disabled></el-input>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="handleCancel">取 消</el-button>
        <el-button type="primary" @click="handleEdit">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import LineChart from "../dashboard/admin/components/LineChart";

export default {
  data() {
    return {
      id: null,

      // 标识信息
      idTableData: [
        { id: 1, name: "水电站1", locate: "空间维度1" },
        // { id: 2, name: "水电站2", locate: "空间维度2" },
      ],
      idTableColumns: [
        { prop: "id", label: "ID" },
        { prop: "name", label: "名称" },
        { prop: "locate", label: "空间维度" },
      ],

      // 特征信息
      feaTableData: [
        {
          area: "流域1",
          river: "河流1",
          totalStorage: "总库容1",
          adjustStorage: "调节库容1",
          floodStorage: "防洪库容1",
          unit: "业主单位1",
          controller: "实控人1",
        },
        // {
        //   area: "流域2",
        //   river: "河流2",
        //   totalStorage: "总库容2",
        //   adjustStorage: "调节库容2",
        //   floodStorage: "防洪库容2",
        //   unit: "业主单位2",
        //   controller: "实控人2",
        // },
        // {
        //   area: "流域3",
        //   river: "河流3",
        //   totalStorage: "总库容3",
        //   adjustStorage: "调节库容3",
        //   floodStorage: "防洪库容3",
        //   unit: "业主单位3",
        //   controller: "实控人3",
        // },
      ],
      feaTableColumns: [
        { prop: "area", label: "所属流域" },
        { prop: "river", label: "所属河流" },
        { prop: "totalStorage", label: "总库容" },
        { prop: "adjustStorage", label: "调节库容" },
        { prop: "floodStorage", label: "防洪库容" },
        { prop: "unit", label: "业主单位" },
        { prop: "controller", label: "实控人" },
      ],

      // 时间信息
      dateTableData: [
        { preDate: "2023-9-1", endDate: "2023-10-1" },
        // { preDate: "2023-9-2", endDate: "2023-10-2" },
      ],
      dateTableColumns: [
        { prop: "preDate", label: "生效时间" },
        { prop: "endDate", label: "失效时间" },
      ],

      // 编辑框
      dialogFormVisible: false,
      form: {},
      formLabelWidth: "120px",
    };
  },
  components: { LineChart },
  mounted() {
    this.id = this.$route.params.id;
    this.form = {
      id: this.idTableData[0].id,
      name: this.idTableData[0].name,
      locate: this.idTableData[0].locate,
      area: this.feaTableData[0].area,
      river: this.feaTableData[0].river,
      totalStorage: this.feaTableData[0].totalStorage,
      adjustStorage: this.feaTableData[0].adjustStorage,
      floodStorage: this.feaTableData[0].floodStorage,
      unit: this.feaTableData[0].unit,
      controller: this.feaTableData[0].controller,
      preDate: this.dateTableData[0].preDate,
      endDate: this.dateTableData[0].endDate,
    };
    // 使用传递的参数进行相应的处理
  },
  methods: {
    cellClass() {
      return "bold-text"; // 普通单元格样式类名
    },
    handleConfirm() {
      this.$router.go(-1);
      this.$message({
        message: "删除成功！",
        type: "success",
      });
    },
    handleBack() {
      this.$router.go(-1);
    },
    handleEdit() {
      this.dialogFormVisible = false;
      this.$message({
        message: "编辑成功！",
        type: "success",
      });
      // 这里要注意,只是先写模板，实际情况应该是异步获取数据后更新form
      this.form = {
        id: this.idTableData[0].id,
        name: this.idTableData[0].name,
        locate: this.idTableData[0].locate,
        area: this.feaTableData[0].area,
        river: this.feaTableData[0].river,
        totalStorage: this.feaTableData[0].totalStorage,
        adjustStorage: this.feaTableData[0].adjustStorage,
        floodStorage: this.feaTableData[0].floodStorage,
        unit: this.feaTableData[0].unit,
        controller: this.feaTableData[0].controller,
        preDate: this.dateTableData[0].preDate,
        endDate: this.dateTableData[0].endDate,
      };
    },
    handleCancel() {
      this.dialogFormVisible = false;
      // 相当于有一个副本
      this.form = {
        id: this.idTableData[0].id,
        name: this.idTableData[0].name,
        locate: this.idTableData[0].locate,
        area: this.feaTableData[0].area,
        river: this.feaTableData[0].river,
        totalStorage: this.feaTableData[0].totalStorage,
        adjustStorage: this.feaTableData[0].adjustStorage,
        floodStorage: this.feaTableData[0].floodStorage,
        unit: this.feaTableData[0].unit,
        controller: this.feaTableData[0].controller,
        preDate: this.dateTableData[0].preDate,
        endDate: this.dateTableData[0].endDate,
      };
    },
  },
};
</script>

<style>
.detail {
  padding: 32px;
  background-color: rgb(240, 242, 245);
  position: relative;
}

.myRouter {
  margin: 20px;
}

.routerLink {
  text-align: center;
  margin-top: 20px;
}

.bold-text {
  font-weight: bold;
  /* font-size: large; */
}
</style>