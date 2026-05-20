# kpw_equip_rent_app_ios

A new project.

### 1. **CSS 动画样式（第 10-188 行）**

这部分定义了加载动画的视觉效果：

| 元素/类名 | 作用 |
|-----------|------|
| `#loader-wrapper` | 加载动画的容器，覆盖全屏 |
| `#loader` | 旋转的圆形加载图标（三层嵌套） |
| `.loader-section.section-left/.section-right` | 页面加载完成后向两侧滑出的遮罩层 |
| `.loaded` | 页面加载完成后的状态类，触发退场动画 |

**核心动画原理**：
- `#loader` 使用 CSS `animation: spin` 实现旋转效果
- 页面加载完成后添加 `.loaded` 类，触发退场动画：
  - 左右遮罩向两侧滑出（`translateX(-100%)` 和 `translateX(100%)`）
  - 加载图标淡出（`opacity: 0`）
  - 整个容器向上滑出（`translateY(-100%)`）

---

### 2. **HTML 结构（第 198-206 行）**

```html
<div id="app">
    <div id="loader-wrapper">
        <div id="loader"></div>
        <div class="loader-section section-left"></div>
        <div class="loader-section section-right"></div>
        <div class="load_title">正在加载 一张蓝图系统,请耐心等待</div>
    </div>
</div>
```

**结构说明**：
- `<div id="loader">`：旋转的加载图标
- `<div class="loader-section section-left/right">`：左右两个遮罩层
- `<div class="load_title">`：加载提示文字

---

### 加载动画工作流程：

1. **页面初始化时**：显示蓝色背景 + 白色旋转 loader + 加载提示文字
2. **页面加载完成时**：通过 JavaScript 给 `<body>` 或 `<div id="app">` 添加 `.loaded` 类
3. **退场动画**：
   - 左右遮罩层向两侧滑出（耗时 0.7s，延迟 0.3s）
   - loader 图标淡出（耗时 0.3s）
   - 整个 `#loader-wrapper` 向上滑出（耗时 0.3s，延迟 1s）

---

**总结**：加载动画主要由 **CSS 样式（第 10-188 行）** 和 **HTML 结构（第 198-206 行）** 两部分组成，通过 JavaScript 控制 `.loaded` 类的添加来触发退场动画。
