echartjs

第一章 ECharts简介

ECharts，缩写来自Enterprise Charts，商业级数据图表，一个纯Javascript的图表库，可以流畅的运行在PC和移动设备上，兼容当前绝大部分浏览器（IE6/7/8/9/10/11，chrome，firefox，Safari等），底层依赖轻量级的Canvas类库ZRender，提供直观，生动，可交互，可高度个性化定制的数据可视化图表。创新的拖拽重计算、数据视图、值域漫游等特性大大增强了用户体验，赋予了用户对数据进行挖掘、整合的能力。
支持折线图（区域图）、柱状图（条状图）、散点图（气泡图）、K线图、饼图（环形图）、雷达图（填充雷达图）、和弦图、力导向布局图、地图、仪表盘、漏斗图、事件河流图等12类图表，同时提供标题，详情气泡、图例、值域、数据区域、时间轴、工具箱等7个可交互组件，支持多图表、组件的联动和混搭展现。
开源的ECharts来自百度EFE数据可视化团队
第二章 在angular-martieral项目中如何使用

2.1.1 echarts安装

bower install echarts
npm install ng-echarts
2.1.2 配置的修改

1.将node_module文件夹下面的ng-echarts/dist/ng-echart.js文件复制到将bower_components文件夹下面的echarts/dist下 面，如下图所示：


将bower_components文件夹下面的echarts文件夹下的.bower.json修改为如下所示：


ng-echarts的注入
