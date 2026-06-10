# 技术规范 · 本地闽菜食材筛选菜谱网站

## 技术栈
| 层级 | 技术 | 版本 | 说明 |
|------|------|------|------|
| 结构层 | HTML5 | - | 语义化标签 |
| 样式层 | Tailwind CSS | v3 (CDN) | 原子化 CSS 框架 |
| 逻辑层 | 原生 JavaScript | ES6+ | 无框架依赖 |
| 字体 | Google Fonts | Noto Sans SC | 中文无衬线字体 |
| 图标 | SVG 内嵌 | - | 无图标库依赖 |

## 架构设计

### 文件结构
```
Recipe/
├── index.html          # 主应用（单文件）
├── recipe.json         # 原始数据（50道闽菜）
└── dev-log/            # 开发日志文件夹
    ├── requirements.md # 需求文档
    ├── tech-spec.md    # 技术规范（本文件）
    ├── design-spec.md  # 设计规范
    ├── execution-steps.md # 执行步骤
    └── changelog.md    # 开发日志
```

### 数据流
```
recipe.json 数据
     ↓
JavaScript 内嵌数组 (recipes)
     ↓
用户操作 (输入/点击标签) → selectedIngredients[]
     ↓
filterRecipes() → recipeMatchesAnyIngredient()
     ↓
renderRecipeCards() → DOM 更新
```

### 核心算法

#### 食材匹配（双向模糊匹配）
```
ingredientMatches(recipeIngredient, searchTerm):
  - 两者均转为小写并去空格
  - recipeIngredient 包含 searchTerm  OR  searchTerm 包含 recipeIngredient
  - 例："槟榔芋头" matches "芋头" ✓
  - 例："猪肉馅" matches "猪肉" ✓
```

#### 筛选逻辑
```
filterRecipes():
  if selectedIngredients 为空 → 返回全部
  else → recipes.filter(r =>
    r.mainIngredients 中任一项与 selectedIngredients 中任一项匹配
  )
```

### 组件树
```
App
├── Header (标题、菜谱计数)
├── SearchSection
│   ├── IngredientInput (输入框 + 自动补全下拉)
│   ├── SelectedTags (已选食材标签 + 删除按钮)
│   └── PresetTags (常用食材点击标签)
├── ResultBar (结果统计 + 清除筛选按钮)
├── RecipeGrid
│   └── RecipeCard × N (菜品卡片)
├── EmptyState (空结果占位)
├── DetailModal (详情弹窗)
└── Footer (页脚)
```

### 性能考量
- 纯前端筛选，O(n×m) 复杂度（n=菜谱数，m=选中食材数），数据量小无性能问题
- 无虚拟 DOM，直接操作 DOM
- 自动补全限制最多 8 条建议

### 浏览器兼容性
- 目标：Chrome 90+, Firefox 90+, Safari 15+, Edge 90+
- 使用 ES6+ 语法（const/let、箭头函数、模板字符串）
