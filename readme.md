# WebReport - 前端监控上报工具集

一个完整的前端监控和数据上报解决方案，包含性能监控、错误捕获、用户行为追踪等功能的示例集合。

## 📋 项目概述

本项目展示了前端监控和数据上报的各种实现方式，包括：

- 性能监控（页面加载时间、白屏时间等）
- 错误监控（JavaScript错误、Promise错误）
- 用户行为追踪（点击、输入、页面访问等）
- 多种数据上报方式（Image、Fetch、SendBeacon）

## 🚀 快速开始

### 克隆项目

```bash
git clone https://github.com/xufangfang-99/webReport.git
cd webReport
```

### 直接打开HTML文件

项目中的每个HTML文件都是独立的示例，可以直接在浏览器中打开查看效果。

## 📁 文件说明

### 1. `1.performanc.html` - 性能监控

展示如何使用 Performance API 监控页面加载性能：

- 页面加载时间计算
- Navigation Timing API 使用示例
- 兼容性处理方案

### 2. `2.error.html` - 错误捕获

演示前端错误监控的实现：

- `window.onerror` 捕获 JavaScript 运行时错误
- `unhandledrejection` 事件捕获未处理的 Promise 错误
- 错误信息收集和处理

### 3. `3.fetch.html` - Fetch 请求监控

展示如何拦截和监控 Fetch 请求：

- Fetch API 的包装和拦截
- HTTP 错误状态码处理
- 请求失败的统一处理

### 4. `4.reportMessage.html` - 完整埋点SDK

一个功能完整的埋点工具 SDK 实现：

- **自动埋点**：自动捕获点击、输入、选择等用户行为
- **手动埋点**：提供 API 进行自定义事件上报
- **性能监控**：自动收集页面性能数据
- **错误监控**：集成错误捕获功能
- **批量上报**：支持事件队列和批量发送
- **可视化日志**：在页面上实时显示埋点日志

### 5. `5.img-report.html` - 图片上报

最简单可靠的数据上报方式：

- 使用 Image 对象发送 GET 请求
- 无跨域限制
- 兼容性最好

### 6. `6.report.html` - 三种上报方式对比

详细对比和演示三种主要的数据上报方式：

- **图片上报**：简单可靠，适合小数据量
- **Fetch上报**：功能强大，支持 POST 和大数据
- **SendBeacon上报**：页面卸载时的最佳选择
- **综合策略**：根据场景自动选择最佳上报方式

### 7. `7.fetch-report.html` - Fetch上报示例

Fetch API 上报的具体实现示例

### 8. `8.send-report.html` - SendBeacon上报示例

SendBeacon API 的使用示例，包含降级处理

## 💡 核心功能

### 埋点SDK功能特性

- ✅ 自动埋点（点击、输入、选择等）
- ✅ 手动埋点 API
- ✅ 性能数据收集
- ✅ 错误自动捕获
- ✅ 批量上报机制
- ✅ 事件队列管理
- ✅ 自定义配置
- ✅ 调试模式

### 上报方式对比

| 方式 | 优势 | 劣势 | 适用场景 |
|------|------|------|----------|
| 图片上报 | 无跨域、兼容性好、实现简单 | 只支持GET、数据量受限 | 普通埋点数据 |
| Fetch上报 | 支持POST、可获取响应、数据格式灵活 | 有跨域限制、页面卸载时可能失败 | 重要数据、需要响应 |
| SendBeacon | 页面卸载时可靠、异步不阻塞 | 无法获取响应、兼容性限制 | 页面离开时的数据 |

## 🔧 使用示例

### 基础埋点SDK使用

```javascript
// 初始化SDK
const tracker = new TrackingSDK({
    debug: true,
    userId: 'user_123',
    autoTrack: true,
    reportUrl: '/api/track'
});

// 手动埋点
tracker.track('custom_event', {
    action: 'button_click',
    value: '提交按钮'
});

// 设置用户ID
tracker.setUserId('new_user_456');

// 手动触发上报
tracker.flush();
```

### 智能上报策略

```javascript
const reporter = new Reporter('https://your-server.com/report');

// 普通上报 - 使用图片方式
reporter.report('用户点击按钮');

// 紧急数据 - 使用Fetch方式
reporter.report('支付成功', { urgent: true });

// 页面卸载 - 使用SendBeacon
window.addEventListener('beforeunload', () => {
    reporter.report('用户离开页面', { onUnload: true });
});
```

## 🎯 最佳实践

1. **选择合适的上报方式**
   - 一般埋点数据使用图片上报
   - 重要业务数据使用 Fetch 上报
   - 页面卸载时必须使用 SendBeacon

2. **批量上报**
   - 设置合理的批量大小（建议 10-20 条）
   - 定时上报 + 数量触发相结合

3. **错误处理**
   - 上报失败时的降级方案
   - 本地缓存机制（注意隐私合规）

4. **性能优化**
   - 避免频繁上报影响页面性能
   - 使用 requestIdleCallback 在空闲时上报

5. **数据安全**
   - 敏感信息脱敏
   - 使用 HTTPS 传输
   - 添加签名验证

## 🌟 特色功能

### 可视化调试

`4.reportMessage.html` 中的 SDK 提供了实时日志展示功能，方便开发调试：

- 实时显示捕获的事件
- 格式化的 JSON 数据展示
- 清晰的时间戳标记

### 智能降级

多种上报方式之间的自动降级：

- SendBeacon 失败自动降级到图片上报
- Fetch 失败自动降级到图片上报
- 浏览器兼容性自动检测

## 📝 注意事项

1. **跨域问题**：Fetch 和 SendBeacon 需要服务器配置 CORS
2. **数据大小**：图片上报受 URL 长度限制（一般 2KB）
3. **浏览器兼容性**：SendBeacon 在 IE 中不支持
4. **页面性能**：避免过于频繁的上报影响用户体验

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

## 📄 许可证

MIT License

## 完整监控平台从指标到可视化全链路体系设计

1，完整链路，服务侧处理也很注重
2. 服务编排细节，CICD的实现
3. 数据传输协议、数据清洗加工、数据统计、数据可视化

### Docker 来编排所有需要使用的服务

- clickhouse
- kafka