# 设计规范 · 本地闽菜食材筛选菜谱网站

## 设计理念
极简干净 · 闽菜文化 · 现代 UI

## 色彩系统

| Token | 色值 | 用途 |
|-------|------|------|
| `minred` (主色) | `#c8161d` | 按钮、高亮、品牌色 |
| `minred-dark` (深色) | `#a01217` | 按钮 hover、激活态 |
| `minred-light` (浅色) | `#fde8e9` | 标签背景、卡片高亮 |
| `minred-50` | `#fef2f2` | 最浅背景 |
| 背景色 | `#fafaf9` (stone-50) | 页面主背景 |
| 卡片白 | `#ffffff` | 卡片、输入区背景 |
| 文字主色 | `#1c1917` (stone-900) | 标题 |
| 文字次色 | `#57534e` (stone-600) | 副文本 |
| 文字辅助 | `#a8a29e` (stone-400) | 提示文字 |
| 边框色 | `#e7e5e4` (stone-200) | 卡片、输入框边框 |

## 字体排版

| 层级 | 字号 | 字重 | 用途 |
|------|------|------|------|
| H1 | 24-28px | 700 | 页面主标题 |
| H2 | 20px | 700 | 菜谱名 |
| Body | 14-16px | 400 | 正文 |
| Small | 12-13px | 400-500 | 标签、辅助信息 |
| Caption | 10-11px | 400 | 微小标注 |

字体族：`'Noto Sans SC', -apple-system, BlinkMacSystemFont, sans-serif`

## 组件规范

### 卡片 (Recipe Card)
- 圆角：`border-radius: 16px` (rounded-2xl)
- 边框：`1px solid #e7e5e4`
- 内边距：`20px`
- hover 效果：`translateY(-4px)` + 阴影增强
- 阴影：`0 20px 40px -12px rgba(200, 22, 29, 0.15)`
- 过渡：`0.3s cubic-bezier(0.4, 0, 0.2, 1)`

### 按钮
- 主按钮：`#c8161d` 背景，白色文字，`border-radius: 12px`
- hover：加深至 `#a01217`，阴影增强
- active：`scale(0.95)` 反馈
- 标签按钮：轮廓样式，选中后填充

### 输入框
- 圆角：`12px` (rounded-xl)
- 边框：`2px solid #e7e5e4`
- 聚焦：边框变 `#c8161d`，外发光 `ring-4 ring-minred/10`

### 弹窗 (Modal)
- 遮罩：`rgba(0,0,0,0.5)` + `backdrop-filter: blur(4px)`
- 内容区：白色背景，圆角 16px，最大高度 85vh
- 进入动画：`slideUp 0.35s`（从下往上 + 缩放）

### 难度标签
- 简单：绿色 `#dcfce7` 背景 + `#166534` 文字
- 中等：黄色 `#fef3c7` 背景 + `#92400e` 文字
- 困难：红色 `#fde8e9` 背景 + `#991b1b` 文字

## 布局规范
- 最大宽度：`1280px` (max-w-7xl)
- 水平内边距：响应式 `16px / 24px / 32px`
- 卡片网格：`1 列(mobile) → 2 列(tablet) → 3 列(desktop)`
- 间距：`gap: 16-20px`

## 交互规范
- 所有可点击元素有 hover 状态变化
- 过渡动画使用 `cubic-bezier(0.4, 0, 0.2, 1)` 缓动
- 弹窗打开时禁止 body 滚动
- ESC 键关闭弹窗
- 点击遮罩区关闭弹窗
