<template>
  <div id="container"></div>
</template>

<script>
export default {
  mounted() {
    window._AMapSecurityConfig = {
      securityJsCode: "7c7164868d32a7bbeae45d5850ca954b", // 「您申请的安全密钥」
    };

    AMapLoader.load({
      key: "c28c19846c55b89384b80964a11e8028", // 申请好的Web端开发者Key，首次调用 load 时必填
      version: "2.0", // 指定要加载的 JSAPI 的版本，缺省时默认为 1.4.15
    })
      .then((AMap) => {
        // 初始化地图
        const map = new AMap.Map("container", {
          center: [111.0075, 30.8233],
          zoom: 9,
          layers: [
            new AMap.TileLayer.Satellite(),
            new AMap.TileLayer.RoadNet(),
          ],
        });

        // 水电站标点
        const markers = [
          [111.0075, 30.8233], // 三峡水电站
          [110.3211, 31.0368],
          [108.4685, 30.8324],
          [112.1845, 30.3068],
          [114.8778, 30.4209],
          [113.4421, 29.7715],
        ];
        markers.forEach((position) => {
          const marker = new AMap.Marker({
            position: position,
            content: "<img src='./水电站.png'>",
            offset: new AMap.Pixel(-12, -12),
          });
          marker.setTitle("水电站");
          map.add(marker);
        });


        // 地图控件
        AMap.plugin(
          [
            "AMap.ToolBar",
            "AMap.Scale",
            "AMap.HawkEye",
            "AMap.MapType",
            "AMap.ControlBar",
          ],
          function () {
            // ToolBar(工具条): 集成了缩放, 平移, 定位
            map.addControl(new AMap.ToolBar());

            // Scale(比例尺): 展示地图在当前层级和经纬度下的比例
            map.addControl(new AMap.Scale());

            // HawkEye(鹰眼): 右下角地图的缩略图
            // map.addControl(new AMap.HawkEye());

            // map.addControl(new AMap.MapType())

            map.addControl(new AMap.ControlBar());
          }
        );
      })
      .catch((e) => {
        console.error(e); //加载错误提示
      });
  },
};
</script>

<style>
#container {
  width: 100%;
  height: 100%;
}
</style>