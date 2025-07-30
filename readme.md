# 前端性能异常监控与埋点平台全栈架构与实践

## 前端项目的整体稳定性是怎么保证的？异常和性能的监控 SDK 内核如何实现？

一、稳定性
1，性能采、异常采集、用户行为埋点 SDK 开发
2，数据上报协议
3，数据统计清洗与加工
4，可视化

二，SDK实现细节
1，性能、异常指标设计
2，上报逻辑，图片上报、sendbacon、fetch
3，用户自定义指标数据

### 性能指标

1.页面加载
    - FP(First Paint) 首次渲染
      评估工具：Chrome DevTools Performance面板。
    - FCP(First Contentful Paint) 首次内容绘制
      评估工具：Performance面板、web-vitals或Lightthouse
    - LCP(Largest Contentful Paint) 最大内容绘制
      理想值：<2.5秒
    - TTFB(Time to First Byte) - 首字节到达时间
      评估工具：Network面板。

2.交互性能
    - INP(Interaction to next Paint)-交互到下一次绘制，理想值 <200ms
    - CLS(Cumulative Layout Shift) 累计布局偏移 < 0.1

3.补充指标
    - DNS 查询时间
    - 资源加载时间
    - 长任务时间，数量
  
    - 如何计算得来？
    - 能过 Performance API获取

## 异常指标

1.代码运行时异常
2.Promise rejec异常
3.请求异常
4.资源加载异常

### 代码运行时异常如何捕获并上报途径

1，图片上报
2，fetch上报
3，sendBeacon上报

### 用户行为指标--用户行为埋点

- 埋点的实现方式有如下三种：
1，无痕埋点
2，可视化埋点
3，手动埋点
