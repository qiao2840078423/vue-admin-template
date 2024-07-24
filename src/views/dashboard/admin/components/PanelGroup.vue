<template>
  <div>
    <el-row :gutter="20" class="panel-group">
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-people">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">梯级电站</div>
            <count-to
              :start-val="0"
              :end-val="102400"
              :duration="2600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-message">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">水库</div>
            <count-to
              :start-val="0"
              :end-val="81212"
              :duration="3000"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-money">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">水电站</div>
            <count-to
              :start-val="0"
              :end-val="9280"
              :duration="3200"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-shopping">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">子水电站</div>
            <count-to
              :start-val="0"
              :end-val="13600"
              :duration="3600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-people">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">机组</div>
            <count-to
              :start-val="0"
              :end-val="102400"
              :duration="2600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-message">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">闸门</div>
            <count-to
              :start-val="0"
              :end-val="81212"
              :duration="3000"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-money">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">船闸</div>
            <count-to
              :start-val="0"
              :end-val="9280"
              :duration="3200"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-shopping">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">流域</div>
            <count-to
              :start-val="0"
              :end-val="13600"
              :duration="3600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
    </el-row>
    <el-row :gutter="20" class="panel-group">
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-people">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">河段</div>
            <count-to
              :start-val="0"
              :end-val="102400"
              :duration="2600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-message">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">断面</div>
            <count-to
              :start-val="0"
              :end-val="81212"
              :duration="3000"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-money">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">线路</div>
            <count-to
              :start-val="0"
              :end-val="9280"
              :duration="3200"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-shopping">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">大坝</div>
            <count-to
              :start-val="0"
              :end-val="13600"
              :duration="3600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-people">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">码头</div>
            <count-to
              :start-val="0"
              :end-val="102400"
              :duration="2600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-message">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">水文站</div>
            <count-to
              :start-val="0"
              :end-val="81212"
              :duration="3000"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuidian')">
          <div class="card-panel-icon-wrapper icon-money">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">气象站</div>
            <count-to
              :start-val="0"
              :end-val="9280"
              :duration="3200"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
      <el-col :xs="6" :sm="6" :lg="3" class="card-panel-col">
        <div class="card-panel" @click="handleSetTableData('shuiwen')">
          <div class="card-panel-icon-wrapper icon-shopping">
            <svg-icon icon-class="shuidianzhan" class-name="card-panel-icon" />
          </div>
          <div class="card-panel-description">
            <div class="card-panel-text">水质站</div>
            <count-to
              :start-val="0"
              :end-val="13600"
              :duration="3600"
              class="card-panel-num"
            />
          </div>
        </div>
      </el-col>
    </el-row>
  </div>
</template>

<script>
import CountTo from "vue-count-to";

export default {
  components: {
    CountTo,
  },
  methods: {
    handleSetTableData(type) {
      this.$router.push(`/data/search/${type}`);
    },
  },
};
</script>

<style lang="scss" scoped>
.panel-group {
  margin-top: 9px;

  .card-panel-col {
    margin-bottom: 16px;
  }

  .card-panel {
    height: 108px;
    cursor: pointer;
    font-size: 12px;
    position: relative;
    overflow: hidden;
    color: #666;
    background: #fff;
    box-shadow: 4px 4px 40px rgba(0, 0, 0, 0.05);
    border-color: rgba(0, 0, 0, 0.05);

    &:hover {
      .card-panel-icon-wrapper {
        color: #fff;
      }

      .icon-people {
        background: #40c9c6;
      }

      .icon-message {
        background: #36a3f7;
      }

      .icon-money {
        background: #f4516c;
      }

      .icon-shopping {
        background: #34bfa3;
      }
    }

    .icon-people {
      color: #40c9c6;
    }

    .icon-message {
      color: #36a3f7;
    }

    .icon-money {
      color: #f4516c;
    }

    .icon-shopping {
      color: #34bfa3;
    }

    .card-panel-icon-wrapper {
      width: 30%;
      float: left;
      margin: 20px 0 0 5%;
      padding: 5%;
      transition: all 0.38s ease-out;
      border-radius: 6px;
    }

    .card-panel-icon {
      float: left;
      font-size: 35px;
    }

    .card-panel-description {
      width: 50%;
      float: right;
      font-weight: bold;
      margin: 25px 8% 15px 0px;

      .card-panel-text {
        line-height: 18px;
        // color: rgba(0, 0, 0, 0.45);
        color: #666464;
        font-size: 15px;
        margin-bottom: 12px;
      }

      .card-panel-num {
        font-size: 17px;
      }
    }
  }
}

@media (max-width: 550px) {
  .card-panel-description {
    display: none;
  }

  .card-panel-icon-wrapper {
    float: none !important;
    width: 100%;
    height: 100%;
    margin: 0 !important;

    .svg-icon {
      display: block;
      margin: 14px auto !important;
      float: none !important;
    }
  }
}
</style>
