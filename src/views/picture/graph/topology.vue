<!-- 展示界面vue -->
<template>
  <div class="container">
    <div :class="{ blurred: isBlurred }" id="graph-container">
      <!-- 节点面板 -->
      <div class="node_panel">
        <div v-for="item in nodeList" :key="item.code" class="node_li">
          <div
            :class="['item_shape', item.code]"
            draggable="true"
            @dragend="addNode(item.detail, $event)"
          ></div>
          <div>{{ item.detail.data.property }}</div>
        </div>
      </div>

      <!-- 画布显示数据库中的节点 -->

      <div id="map-container">
        <div id="g6-toolbar"></div>
        <div id="minimap-container"></div>
        <div id="search">
          <el-input
            id="search—text"
            placeholder="请输入节点名字搜索"
            prefix-icon="el-icon-search"
            v-model="nodename"
            maxlength="6"
            @keydown.enter.native="search"
          ></el-input>
          <!-- <input id="mytext" v-model="nodename" type="text" name="username" placeholder="请输入节点名字搜索" maxlength="6" @keydown.enter="search"> -->
          <el-button
            id="search-button"
            type="primary"
            icon="el-icon-search"
            @click="search"
            >搜索</el-button
          >
        </div>
      </div>
    </div>

    <!-- 节点详细信息侧边栏 v-if判断 -->
    <el-drawer
      v-if="isNode"
      :visible.sync="drawer"
      :direction="rtl"
      size="15%"
      :modal="true"
      :modal-append-to-body="false"
      :append-to-body="true"
      :wrapperClosable="false"
      :z-index="10"
    >
      <template slot="title">
        <div>
          <!-- 标题内容 -->
          <span style="margin-right: 15px; font-weight: 900; font-size: large"
            >基本信息</span
          >
          <router-link :to="`/detail/${form.id}`">
            <el-button type="text" size="medium">详情</el-button>
          </router-link>
        </div>
      </template>
      <div class="demo-drawer__content">
        <!-- <div style="margin: 20px"></div> -->
        <el-form
          :model="form"
          :label-position="top"
          :inline="true"
          class="myForm"
        >
          <el-form-item label="节点名称">
            <el-input v-model="form.name" autocomplete="on"></el-input>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="节点类型">
            <el-select
              v-model="form.property"
              placeholder="请选择节点类型"
              autocomplete="on"
            >
              <el-option label=" " value=" "></el-option>
              <el-option label="水电站" value="水电站"></el-option>
              <el-option label="水文站" value="水文站"></el-option>
              <el-option label="水位站" value="水位站"></el-option>
              <el-option label="重要水文站" value="重要水文站"></el-option>
            </el-select>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="空间维度">
            <el-input v-model="form.location" autocomplete="on"></el-input>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="生效时间">
            <el-input
              v-model="form.preDate"
              autocomplete="on"
              :disabled="true"
            ></el-input>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="失效时间">
            <el-input
              v-model="form.endDate"
              autocomplete="on"
              :disabled="true"
            ></el-input>
          </el-form-item>
        </el-form>
        <div style="margin: 60px"></div>
        <div class="demo-drawer__footer">
          <el-button @click="cancelForm">取 消</el-button>
          <el-popconfirm
            title="确定编辑吗？"
            @onConfirm="changeNodeInfo"
            class="myForm"
          >
            <el-button slot="reference" type="primary">编 辑</el-button>
          </el-popconfirm>
        </div>
      </div>
    </el-drawer>
    <!-- 边详细信息侧边栏 v-if判断 -->
    <el-drawer
      v-else
      :visible.sync="drawer"
      :direction="rtl"
      size="15%"
      :modal="true"
      :modal-append-to-body="false"
      :append-to-body="true"
      :wrapperClosable="false"
      :z-index="10"
    >
      <template slot="title">
        <div>
          <!-- 标题内容 -->
          <span style="margin-right: 15px; font-weight: 900; font-size: large"
            >基本信息</span
          >
          <router-link :to="`/detail/${form.id}`">
            <el-button type="text" size="medium">详情</el-button>
          </router-link>
        </div>
      </template>
      <div class="demo-drawer__content">
        <!-- <div style="margin: 20px"></div> -->
        <el-form
          :model="form"
          :label-position="top"
          :inline="true"
          class="myForm"
        >
          <el-form-item label="起点名称">
            <el-input
              v-model="form.start"
              autocomplete="on"
              :disabled="true"
            ></el-input>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="终点名称">
            <el-input
              v-model="form.end"
              autocomplete="on"
              :disabled="true"
            ></el-input>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="流动时间">
            <el-input v-model="form.time" autocomplete="on"></el-input>
          </el-form-item>
          <div style="margin: 20px"></div>
          <el-form-item label="河道长度">
            <el-input v-model="form.distance" autocomplete="on"></el-input>
          </el-form-item>
        </el-form>
        <div style="margin: 60px"></div>
        <div class="demo-drawer__footer">
          <el-button @click="cancelForm">取 消</el-button>
          <el-popconfirm
            title="确定编辑吗？"
            @onConfirm="changeEdgeInfo"
            class="myForm"
          >
            <el-button slot="reference" type="primary">编 辑</el-button>
          </el-popconfirm>
        </div>
      </div>
    </el-drawer>
  </div>
</template>
  
  
<script>
import G6 from "@antv/g6";

export default {
  name: "Graph",
  // data用于存储全局数据
  // g：绘图对象
  // isNode：用于控制侧边栏内容，与css配合使用
  // drawer：是否弹出侧边栏
  // x,y： 坐标
  // form：当前具体对象信息
  // nodeList： 各种节点样式
  data() {
    return {
      g: null,
      isNode: false,
      dialogFormVisible: false,
      drawer: false, // 抽屉是否打开
      isBlurred: false, // 是否虚化
      x: "",
      y: "",
      form: {
        id: "",
        name: "",
        property: "",
        start: "",
        end: "",
        time: " ",
        distance: " ",
        location: "空间维度1",
        preDate: "生效时间",
        endDate: "失效时间",
      },
      nodename: "",
      data: {
        nodes: [],
        edges: [],
      },
      // 节点样式示例
      nodeList: [
        {
          code: "shuidianzhan",
          detail: {
            size: [90, 60],
            data: {
              name: "",
              property: "水电站",
            },
            type: "ellipse",
            style: {
              fill: "green",
              stroke: "green",
            },
          },
        },
        {
          code: "shuiwenzhan",
          detail: {
            size: [90, 60],
            data: {
              name: "",
              property: "水文站",
            },
            type: "rect",
            style: {
              fill: "skyblue",
              stroke: "skyblue",
            },
          },
        },
        {
          code: "important",
          detail: {
            size: [90, 60],
            data: {
              name: "",
              property: "重要水文站",
            },
            type: "rect",
            style: {
              fill: "pink",
              stroke: "pink",
            },
          },
        },
        {
          code: "shuiweizhan",
          detail: {
            size: [100, 75],
            data: {
              name: "",
              property: "水位站",
            },
            type: "diamond",
            style: {
              fill: "rgb(232, 176, 150)",
              stroke: "rgb(232, 176, 150)",
            },
          },
        },
      ],
    };
  },

  methods: {
    // 方法：关闭侧边栏
    cancelForm() {
      this.drawer = false;
    },
    // 方法：添加节点
    addNode(type, e) {
      // 将屏幕/页面坐标转换为渲染坐标
      const point = this.g.getPointByClient(e.x, e.y);
      const model = {
        id: "node" + Math.random(), // id使用了随机数，尽可能避免重复,写一方法获取最大id
        label: "", // 文本标签
        size: type.size,
        type: type.type,
        data: type.data,
        style: type.style,
        labelCfg: {
          style: {
            fontSize: 22,
          },
        },
        x: point.x,
        y: point.y,
      };

      this.g.addItem("node", model, false);
    },
    // 方法：修改节点内容
    changeNodeInfo() {
      const node = this.g.findById(this.form.id);
      if (this.form.property == "水文站") {
        this.g.updateItem(node, {
          label: this.form.name,
          data: {
            name: this.form.name,
            property: this.form.property,
          },
          type: "rect",
          style: {
            fill: "skyblue",
            stroke: "skyblue",
          },
        });
      } else if (this.form.property == "重要水文站") {
        this.g.updateItem(node, {
          label: this.form.name,
          data: {
            name: this.form.name,
            property: this.form.property,
          },
          type: "rect",
          style: {
            fill: "pink",
            stroke: "pink",
          },
        });
      } else if (this.form.property == "水位站") {
        this.g.updateItem(node, {
          label: this.form.name,
          data: {
            name: this.form.name,
            property: this.form.property,
          },
          type: "diamond",
          style: {
            fill: "skyblue",
            stroke: "skyblue",
          },
        });
      } else if (this.form.property == "水电站") {
        this.g.updateItem(node, {
          label: this.form.name,
          data: {
            name: this.form.name,
            property: this.form.property,
          },
          type: "ellipse",
          style: {
            fill: "green",
            stroke: "green",
          },
        });
      } else {
        this.g.updateItem(node, {
          label: this.form.name,
          data: {
            name: this.form.name,
            property: this.form.property,
          },
          type: "circle",
          style: {
            fill: "red",
            stroke: "red",
          },
        });
      }
      this.drawer = false;
      this.$message({
        message: "编辑成功！",
        type: "success",
      });
    },

    //方法： 更改边内容
    changeEdgeInfo() {
      const edge = this.g.findById(this.form.id);
      this.g.updateItem(edge, {
        label: this.form.distance,
        data: {
          distance: this.form.distance,
          time: this.form.time,
        },
      });
      this.drawer = false;
      this.$message({
        message: "编辑成功！",
        type: "success",
      });
    },

    // 查询节点并将画布以查询节点中心展示
    search() {
      console.log(this.nodename);
      let foundNodes = [];
      foundNodes = this.data.nodes.filter((item) => {
        if (item.data.name === this.nodename) {
          let nodeId = item.id;
          this.g.focusItem(item.id);

          // // 动画地移动
          // this.g.focusItem(item.id, true);
          let foundNode = this.g.findById(nodeId);

          // console.log(foundNode.getBBox());
          this.g.focusItem(item.id, true, {
            easing: "easeCubic",
            duration: 400,
          });
          let nodex = foundNode.getBBox().centerX;
          let nodey = foundNode.getBBox().centerY;
          const point = this.g.getCanvasByPoint(nodex, nodey);
          const point2 = this.g.getClientByPoint(nodex, nodey);
          console.log(nodex, nodey);
          console.log(point);
          console.log(point2);
          // this.g.zoomTo(1.1);
          this.g.setItemState(foundNode, "active", true);

          return item.data.name === this.nodename;
        }
      });
      console.log(foundNodes);
      if (foundNodes.length == 0) alert("该节点不存在");
    },

    testCoo() {
      const testnode = this.data.nodes[1];
      console.log(this.data.nodes[1].data.name);
      console.log(this.data.nodes[1].id);
    },

    async fetchData() {
      //neo4j查询语句，引入neo4j模块

      var nodeQuery = "MATCH(n:NodeEntity) RETURN n";
      var neo4j = require("neo4j-driver");

      //从本地neo4j数据库读取数据
      this.driver = neo4j.driver(
        "neo4j://localhost:7687",
        neo4j.auth.basic("neo4j", "031106")
      );

      let me = this;
      me.records = [];
      this.clearAll = true;
      let nodeSession = this.driver.session();
      nodeSession
        .run(nodeQuery, {})
        .then((result) => {
          me.records = result.records;
          //遍历记录，获得数据
          //console.log(me.records)
          for (let i = 0; i < me.records.length; i++) {
            //properties是指节点信息
            var getLine = me.records[i]._fields[0].properties;

            //根据数据创建节点tmpNode临时节点
            var tmpNode = {
              id: "Node" + getLine.id,
              label: getLine.name,
              size: [90, 60],
              type: "",
              style: {},
              labelCfg: {
                style: {
                  fontSize: 22,
                },
              },

              data: {
                name: getLine.name,
                property: getLine.property,
                uuid: parseInt(getLine.id),
              },
            };
            if (getLine.property == "水文站") {
              tmpNode.type = "rect";
              tmpNode.style = {
                fill: "skyblue",
                stroke: "skyblue",
              };
            } else if (getLine.property == "重要水文站") {
              tmpNode.type = "rect";

              tmpNode.style = {
                fill: "pink",
                stroke: "pink",
              };
            } else if (getLine.property == "水位站") {
              tmpNode.type = "diamond";
              tmpNode.size = [100, 75];
              tmpNode.style = {
                fill: "rgb(232, 176, 150)",
                stroke: "rgb(232, 176, 150)",
              };
            } else if (getLine.property == "水电站") {
              tmpNode.type = "ellipse";
              tmpNode.style = {
                fill: "green",
                stroke: "green",
              };
            } else {
              tmpNode.type = "circle";
              tmpNode.style = {
                fill: "red",
                stroke: "red",
              };
            }

            // console.log(tmpNode.id);
            this.data.nodes.push(tmpNode);
            // console.log(data.nodes);
          }
          nodeSession.close();
        })
        .catch(function (error) {
          console.log("Cypher 执行失败！", error);
          me.driver.close();
        });
      console.log(this.data.nodes);
    },
  },

  watch: {
    // 监听抽屉是否打开
    drawer(newVal) {
      if (newVal) {
        // 抽屉打开设置主界面虚化
        this.isBlurred = true;
      } else this.isBlurred = false;
    },
  },

  async mounted() {
    // 配置工具栏
    const toolbar = new G6.ToolBar({
      container: "g6-toolbar",

      // position: {x:window.innerWidth/2, y:window.innerHeight - 20},
      // position: {x:,y:},
      //   getContent: () => {
      //   return `
      //     <ul>
      //       <li code='add'>增加节点</li>
      //       <li code='undo'>撤销</li>
      //     </ul>
      //   `
      // },
      //   handleClick: (code, graph) => {
      //     if (code === 'add') {
      //       graph.addItem('node', {
      //         id: 'node2',
      //         label: 'node2',
      //         x: 300,
      //         y: 150
      //       })
      //     } else if (code === 'undo') {
      //       // 自定义 undo
      //       toolbar.undo()
      //       toolbar.autoZoom()
      //     } else {
      //       // 其他操作保持默认不变
      //       toolbar.handleDefaultOperator(code)
      //     }
      //   }
    });

    // 配置缩略图
    let minimapRatio = 4;
    const minimap = new G6.Minimap({
      container: "minimap-container",
      size: [300, 200],
    });

    const menuThis = this;
    /// 配置右键菜单
    const menu = new G6.Menu({
      shouldBegin(evt) {
        return evt.target;
      },
      getContent() {
        return `
            <div data-command="delete">删除</div>
          `;
      },
      handleMenuClick(target, item) {
        const command = target.getAttribute("data-command");
        if (command === "delete") {
          //console.log(222,this);
          //console.log(this.g.getNodes().length);
          menuThis.g.removeItem(item);
        }
      },
    });

    //配置画布
    this.g = new G6.Graph({
      container: "map-container",
      enabledStack: true,

      layout: {
        type: "dagre",
        rankdir: "LR",
        align: "UL",
        nodesep: 15,
        ranksep: 30,
      },
      modes: {
        default: ["drag-canvas", "zoom-canvas", "click-select", "drag-node"],
        //edit: ['click-select'],
      },
      plugins: [menu, toolbar, minimap],
      width: window.innerWidth - 80,
      height: window.innerHeight,
      fitView: true,
    });

    await this.fetchData(); // 等待 fetchData 函数完成
    var neo4j = require("neo4j-driver");
    this.g.moveTo(0, 0);
    //从本地neo4j数据库读取数据
    this.driver = neo4j.driver(
      "neo4j://localhost:7687",
      neo4j.auth.basic("neo4j", "123456")
    );

    let me = this;
    me.records = [];
    var query = "MATCH(n1:NodeEntity)-[m:rel]->(n2:NodeEntity) return m,n1,n2";
    let session = this.driver.session();
    if (query == "") return result.records;

    session
      .run(query, {})
      .then((result) => {
        me.clearAll = false;
        me.records = result.records;

        console.info(me.records);

        //读取每条记录，将相应的边导入图中
        for (let i = 0; i < me.records.length; i++) {
          var startId = "Node" + me.records[i]._fields[1].properties.id;
          var endId = "Node" + me.records[i]._fields[2].properties.id;
          // console.log(startId);
          var tmpEdge = {
            source: startId,
            target: endId,
            label: me.records[i]._fields[0].properties.distance,
            data: {
              distance: me.records[i]._fields[0].properties.distance,
              time: me.records[i]._fields[0].properties.time,
              id: parseInt(me.records[i]._fields[2].properties.id),
            },
            style: {
              lineWidth: 5,
              opacity: 0.6,
              // fill: "black",
              stroke: "	#C0C0C0",
              // 箭头的style
              endArrow: {
                path: G6.Arrow.triangle(1, 2, 0), //宽度、长度、偏移量
                d: 0,
                fill: "#000",
                stroke: "#000",
                opacity: 0.4,
                lineWidth: 3,
                // ...
              },
            },
            labelCfg: {
              style: {
                fontSize: 15,
              },
            },
          };
          this.data.edges.push(tmpEdge);
        }

        this.g.data(this.data);
        this.g.render();
        // console.log(this.g.getNodes().length);
        // console.log(this.data.nodes.length);

        //控制选中边和节点时的高亮状态
        this.g.on("node:mouseenter", (e) => {
          this.g.setItemState(e.item, "active", true);
          console.log(e.item.getBBox().centerX, e.item.getBBox().centerY);
        });
        this.g.on("node:mouseleave", (e) => {
          this.g.setItemState(e.item, "active", false);
        });
        this.g.on("edge:mouseenter", (e) => {
          this.g.setItemState(e.item, "active", true);
        });
        this.g.on("edge:mouseleave", (e) => {
          this.g.setItemState(e.item, "active", false);
        });
        this.g.on("mousemove", (e) => {
          // 获取鼠标的坐标
          const { x, y } = e;
          console.log(e.x, e.y);
          let px = this.g.getClientByPoint(e.x, e.y);

          let cx = this.g.getCanvasByPoint(e.x, e.y);

          console.log("画布坐标", cx.x, cx.y);
          console.log("渲染指标", e.x, e.y);
          console.log("浏览器坐标", px.x, px.y);
          const point = this.g.getViewPortCenterPoint();
          console.log("视口中心的绘制坐标是", point.x, point.y);
          const point2 = this.g.getGraphCenterPoint();
          console.log("图内容中心的绘制坐标是", point2.x, point2.y);
          console.log(this.g.getZoom());
        });

        this.testCoo();

        ///新增边的方法
        // 选中的节点
        let selectedNodes = [];

        // 用于储存新建的边的起始点和终止点
        let sourceNode = null;
        let targetNode = null;

        // 创建边的起始节点和结束节点
        this.g.on("node:click", (e) => {
          const node = e.item;
          const ctrlKey = e.originalEvent.ctrlKey;

          this.form.id = node._cfg.model.id;
          this.form.name = node._cfg.model.data.name;
          this.form.property = node._cfg.model.data.property;
          //console.log(this.form.property);
          this.isNode = true;

          if (ctrlKey) {
            this.drawer = false;
            // 如果按下了Ctrl键，则选中节点
            node.toFront();
            node.setState("selected", true);

            selectedNodes.push(node);

            // 如果选中了两个节点，则在它们之间创建一条边
            if (selectedNodes.length === 2) {
              sourceNode = selectedNodes[0];
              targetNode = selectedNodes[1];
              this.g.addItem("edge", {
                shape: "polyline",
                source: sourceNode,
                target: targetNode,
                label: "",
                style: {
                  endArrow: {
                    path: G6.Arrow.triangle(1, 2, 0), //宽度、长度、偏移量
                    d: 0,
                    fill: "#000",
                    stroke: "#000",
                    opacity: 0.4,
                    lineWidth: 3,
                    // ...
                  },
                },
                labelCfg: {
                  style: {
                    fontSize: 10,
                  },
                },
              });
              this.g.getNodes().forEach((n) => {
                n.clearStates("selected");
              });
              selectedNodes = [];
              sourceNode = null;
              targetNode = null;
            }
          } else {
            this.drawer = true;
            // 如果没有按下Ctrl键，则取消选择所有节点
            this.g.getNodes().forEach((n) => {
              n.clearStates("selected");
            });
            selectedNodes = [];
            sourceNode = null;
            targetNode = null;
          }
        });

        ///修改边的方法
        this.g.on("edge:click", (e) => {
          this.form.id = e.item._cfg.model.id;
          this.drawer = true;
          this.isNode = false;
          const edge = e.item._cfg.model;
          this.form.start = this.g.findById(edge.source).getModel().label;
          this.form.end = this.g.findById(edge.target).getModel().label;
          this.form.time = edge.data.time;
          this.form.distance = edge.data.distance;
        });

        //右键画布的方法，可以无视
        this.g.on("canvas:contextmenu", (evt) => {
          evt.preventDefault();
          //console.log(this.dialogFormVisible);
          this.form.name = "";
          this.form.property = "";
          this.x = evt.canvasX;
          this.y = evt.canvasY;
          this.drawer = false;
          this.dialogFormVisible = true;
        });

        //双击边删除，没有用到
        this.g.on("edge:doubleclick", (e) => {
          this.g.removeItem(e.item._cfg.model);
        });
        session.close();
        me.closeLoading(false);
      })
      .catch(function (error) {
        console.log("Cypher 执行失败！", error);
        me.driver.close();
      });
    //record = this.executeCypher(query);
  },
};
</script>
  
  
<style>
/* 缩略图容器 */
#minimap-container {
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: 1000;
  width: 306px;
  height: 206px;
  background-color: #fff;
  border: 2px solid rgba(192, 192, 192, 0.5);
}

.container {
  width: 100%; /* 设置宽度为父容器的100% */
}

#map-container {
  position: absolute;
  left: 70px;
  background-color: #fff;
  z-index: 1;
  float: left;
  width: 90%;
  height: 100%;
}

#g6-toolbar {
  position: absolute;
  width: 300px;
  height: 50px;
  top: 0;
  left: calc(50% - 150px); /* 水平居中 */
  display: flex;
  justify-content: space-between;
}

#search {
  position: absolute;
  top: 0;
  right: 0px;
  font-size: 15px;
  text-align: center;
  display: flex;
  align-items: center; /* 垂直居中对齐 */
  justify-content: center; /* 水平居中对齐 */
}

#search—text {
  height: 23px;
  font-size: 10px;
}

.el-input__prefix i.el-input__icon {
  /* 使用绝对定位 */
  position: absolute;
  /* 距离输入框左边的距离，根据需要调整 */
  top: 20%;
  /* 垂直居中 */

  transform: translateY(-50%);
}
#search-button {
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 10px;
  width: 50px;
  height: 20px;
}

.blurred {
  filter: blur(1.5px); /* 可以根据需要调整虚化程度 */
}

/* 节点面板 */
.node_panel {
  position: absolute;
  left: 0px;
  top: 50px;
  height: 100%;
  width: 70px;
  box-sizing: border-box;
  padding: 10px 4px;
  border-radius: 4px;
  background-color: #eee;
  box-shadow: 1px 1px 5px #888888;
  z-index: 10;
}

.node_li {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 17px;
  user-select: none;
  font-size: 10px;
}

.el-drawer__wrapper {
  pointer-events: none;
  top: 50px;
}

.el-drawer {
  pointer-events: auto;
}
.demo-drawer__content {
  position: relative;
  left: 5px;
}

:last-child {
  margin-bottom: 0;
}

.shuiwenzhan {
  width: 20px;
  height: 10px;
  background-color: rgb(150, 204, 232);
}

.important {
  width: 20px;
  height: 10px;
  background-color: rgb(245, 194, 203);
}

.shuidianzhan {
  width: 22px;
  height: 11px;
  background-color: rgb(55, 125, 34);
  border-radius: 100%;
  -o-border-radius: 100%;
  -ms-border-radius: 100%;
  -moz-border-radius: 100%;
  -webkit-border-radius: 100%;
}

.shuiweizhan {
  width: 15px;
  height: 15px;
  transform: rotateZ(135deg) skew(30deg, 30deg);
  /* transform: rotateZ(45deg) skew(30deg,30deg); */
  background: rgb(232, 176, 150);
}

.myForm {
  margin-left: 20px;
}

.demo-drawer__footer {
  margin-left: 20px;
}
</style>