# techarts [![Build Status](https://travis-ci.org/elvinzhu/techarts.svg?branch=taro3)](https://travis-ci.org/elvinzhu/techarts)

开箱即用的 Taro3（2.0 请参照 master 分支） echarts 组件. 据有以下特性：

- 支持多种使用方式。
- 支持自定义构建的 echarts
- 支持导出图片

如果你觉得解决了你的问题，并节省了时间，请在 github 上给我一个小星星 ^\_^

### 安装

```javascript
npm install techarts
```

### 使用

```jsx
import EChart from 'techarts';
// 自定义构建的echarts
import * as echarts from './echarts';

// 基本用法
<EChart echarts={echarts} option={option} />;

// 通过组件实例设置数据
<EChart ref={this.chart} echarts={echarts} />

this.chart.current.setOption({...});

// 自定义初始化
<EChart echarts={echarts} onInit={this.onInit} />;

onInit = (canvas, width, height, dpr) => {
  const chart = echarts.init(canvas, null, {
    width: width,
    height: height,
    devicePixelRatio: dpr,
  });
  return chart; // 必须return
};

// 以上三种用法可以结合使用
```

### 参数

| 参数名称     | 解释                                                                                                                             | 默认值 | 是否必填 |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- |
| echarts      | echarts 对象。建议去[官网](https://www.echartsjs.com/zh/builder.html)自定义构建；<br/>注意不要勾选“代码压缩”，可下载后自行压缩。 | -      | Y        |
| option       | 参数同[echart option](https://echarts.apache.org/zh/option.html#title)                                                           | -      | Y        |
| canvasId     | cancas-id 兼容低基础库版本（<2.9.0）时需要                                                                                       | -      | N        |
| disableTouch | 是否禁用手势                                                                                                                     | false  | N        |
| lazyLoad     | 需要拿到组件实例手动 init 的时候请传递 true                                                                                      | false  | N        |
| style        | 样式                                                                                                                             | -      | N        |
| onInit       | 需要自定义 echarts init 时使用                                                                                                   | -      | N        |
| rotated      | transform 选择90°后,如旋转后全屏全屏                                                                                       | -      | N        |
| clickChartFun | 图表点击后动画                                                                               | -      | N        |

### 实例 API

| API 名称             | 参数                                                                                                 | 回调参数  |
| -------------------- | ---------------------------------------------------------------------------------------------------- | --------- |
| init                 | callback                                                                                             | 同 onInit |
| setOption            | [echart option](https://echarts.apache.org/zh/option.html#title)                                     | -         |
| canvasToTempFilePath | 同[小程序](https://developers.weixin.qq.com/miniprogram/dev/api/canvas/wx.canvasToTempFilePath.html) | 同小程序  |
| getCanvasId          | 获取容器 id                                                                                          | -         |

### 示例

参照项目 [demo](https://github.com/elvinzhu/techarts/blob/master/demo/src/pages/index/index.jsx) 目录

### 注意事项

- Taro H5 本地开发时样式加载延时，导致 echarts 初始化宽高读取错误。build 之后正常
- `canvasToTempFilePath` h5 未实现定制宽高位置等功能

### 图表全屏
小程序基础库2.4.0之后可以在json文件中配置pageOrientation来实现小程序的横屏，然后不用修改其他配置直接正常加载图表。这样就不会出现上述问题。
如果是选择直接使用 transform 选择后的全屏
如果通过旋转echarts组件的方式来实现，则会出现touch事件的坐标轴交换的问题。
如果通过交换x轴y轴来实现，则会出现toolbox组件和legend组件无法旋转的问题

### License

MIT[@elvinzhu](https://github.com/elvinzhu)
