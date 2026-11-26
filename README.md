# Simon 的作品集网站

孟菲斯风格个人作品集，含 50 首原创音乐全站随机连播。

## 架构要点

- **壳 + iframe**：`index.html` 是壳，音乐播放器与音频元素驻留壳层永不销毁；页面切换发生在 iframe 内（`location.replace` 不产生历史条目），前进/后退/导航音乐零中断。地址栏与标签标题由 `history.pushState` + postMessage 同步。
- **播放器组件**：注入全部页面的同版代码块。在 iframe 内自动休眠（`.mp-framed` 隐藏 + 脚本 return）；直接打开子页时独立工作，用 sessionStorage 续播兜底。
- **Ogg/Opus 兼容**：`duration === Infinity` 时跳尾骗取真实时长；进度条支持按住拖拽（依赖服务器 Range 支持）。
- **自动播放策略**：进站随机开播；被浏览器拦截时显示提示条，任意点击/按键/触摸激活。
- 13 英寸基准字号 18px；beauty 页图片懒加载；字体自托管；无第三方运行时依赖（仅不蒜子统计）。

## 部署

```
netlify deploy --dir . --prod
```

线上：https://simon-works.netlify.app
