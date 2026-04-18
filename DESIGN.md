# DESIGN.md — 喜茶风格点单网页

## 1. Visual Theme & Atmosphere

**设计哲学**：简洁、时尚、极致 — 还原喜茶 HEYTEA 品牌调性

**氛围关键词**：清新、年轻、极简、时尚、轻盈

**一句话定调**：白色为底、绿色为魂，用最少的元素传递最清晰的信息，让用户在3秒内找到想喝的。

**设计语言**：
- 纯直角/微圆角（4px）为主，传递时尚极简感
- 卡片左边距留白、右边距贴边的不对称版式
- 插画风格图标 + 极简线性图标混搭
- 大面积留白，信息密度克制

---

## 2. Color Palette & Roles

```css
:root {
  /* === 品牌色 === */
  --heytea-green: #00A651;           /* 主品牌绿 */
  --heytea-green-rgb: 0, 166, 81;
  --heytea-green-light: #E8F8EF;     /* 浅绿背景 */
  --heytea-green-light-rgb: 232, 248, 239;
  --heytea-green-dark: #008C44;      /* 深绿/按压态 */
  --heytea-green-dark-rgb: 0, 140, 68;

  /* === 中性色 === */
  --white: #FFFFFF;
  --white-rgb: 255, 255, 255;
  --gray-50: #FAFAFA;
  --gray-50-rgb: 250, 250, 250;
  --gray-100: #F5F5F5;
  --gray-100-rgb: 245, 245, 245;
  --gray-200: #EEEEEE;
  --gray-200-rgb: 238, 238, 238;
  --gray-300: #E0E0E0;
  --gray-300-rgb: 224, 224, 224;
  --gray-400: #BDBDBD;
  --gray-400-rgb: 189, 189, 189;
  --gray-500: #9E9E9E;
  --gray-500-rgb: 158, 158, 158;
  --gray-600: #757575;
  --gray-600-rgb: 117, 117, 117;
  --gray-700: #616161;
  --gray-700-rgb: 97, 97, 97;
  --gray-800: #424242;
  --gray-800-rgb: 66, 66, 66;
  --gray-900: #212121;
  --gray-900-rgb: 33, 33, 33;

  /* === 功能色 === */
  --red: #FF4D4F;
  --red-rgb: 255, 77, 79;
  --orange: #FF8C00;
  --orange-rgb: 255, 140, 0;
  --gold: #FFD700;
  --gold-rgb: 255, 215, 0;

  /* === 语义色 === */
  --bg-primary: var(--white);
  --bg-secondary: var(--gray-50);
  --bg-tertiary: var(--gray-100);
  --text-primary: var(--gray-900);
  --text-secondary: var(--gray-600);
  --text-tertiary: var(--gray-400);
  --border-color: var(--gray-200);
  --accent: var(--heytea-green);
  --accent-hover: var(--heytea-green-dark);
  --accent-bg: var(--heytea-green-light);
}
```

---

## 3. Typography Rules

**字体族**：
```css
/* 中文优先，英文 fallback */
--font-primary: 'PingFang SC', 'Noto Sans SC', 'Helvetica Neue', Arial, sans-serif;
--font-number: 'DIN Alternate', 'NeutraText-DemiAlt', 'Helvetica Neue', sans-serif;
```

**Google Fonts**：
```css
@import url('https://fonts.googleapis.com/css2?family=Noto+Sans+SC:wght@300;400;500;700&display=swap');
```

**字号层级**：

| 层级 | 字号 | 字重 | 行高 | 用途 |
|------|------|------|------|------|
| Display | 28px | 700 | 1.3 | 首页大标题、Banner 标题 |
| H1 | 22px | 700 | 1.4 | 页面主标题 |
| H2 | 18px | 600 | 1.4 | 区块标题 |
| H3 | 16px | 600 | 1.5 | 商品名称 |
| Body | 14px | 400 | 1.6 | 正文、描述 |
| Caption | 12px | 400 | 1.5 | 辅助信息、标签 |
| Price | 20px | 700 | 1.2 | 价格数字（使用数字字体） |
| Price-small | 14px | 600 | 1.2 | 小价格、规格价格 |
| Tag | 11px | 500 | 1.4 | 角标、小标签 |

**禁止**：
- ❌ 全英文页面使用中文字体
- ❌ 标题使用 300 细体（可读性差）
- ❌ 正文低于 12px

---

## 4. Component Stylings

### 4.1 按钮

**主按钮（加入购物车 / 立即下单）**：
```css
.btn-primary {
  background: var(--heytea-green);
  color: var(--white);
  border-radius: 24px;
  padding: 10px 28px;
  font-size: 14px;
  font-weight: 600;
  border: none;
  cursor: pointer;
  transition: all 0.2s ease;
}
.btn-primary:hover {
  background: var(--heytea-green-dark);
  transform: translateY(-1px);
  box-shadow: 0 4px 12px rgba(var(--heytea-green-rgb), 0.3);
}
.btn-primary:active {
  transform: translateY(0);
  box-shadow: none;
}
.btn-primary:disabled {
  background: var(--gray-300);
  color: var(--gray-500);
  cursor: not-allowed;
  transform: none;
  box-shadow: none;
}
.btn-primary:focus-visible {
  outline: 2px solid var(--heytea-green);
  outline-offset: 2px;
}
```

**次要按钮（规格选择）**：
```css
.btn-secondary {
  background: var(--gray-100);
  color: var(--gray-800);
  border-radius: 20px;
  padding: 6px 16px;
  font-size: 13px;
  font-weight: 500;
  border: 1.5px solid transparent;
  cursor: pointer;
  transition: all 0.2s ease;
}
.btn-secondary:hover {
  background: var(--heytea-green-light);
  color: var(--heytea-green);
}
.btn-secondary.active {
  background: var(--heytea-green-light);
  color: var(--heytea-green);
  border-color: var(--heytea-green);
}
.btn-secondary:disabled {
  opacity: 0.4;
  cursor: not-allowed;
}
.btn-secondary:focus-visible {
  outline: 2px solid var(--heytea-green);
  outline-offset: 2px;
}
```

**图标按钮（+/- 数量）**：
```css
.btn-icon {
  width: 28px;
  height: 28px;
  border-radius: 50%;
  border: none;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.15s ease;
  font-size: 16px;
}
.btn-icon.add {
  background: var(--heytea-green);
  color: var(--white);
}
.btn-icon.add:hover {
  background: var(--heytea-green-dark);
  transform: scale(1.1);
}
.btn-icon.minus {
  background: var(--gray-200);
  color: var(--gray-600);
}
.btn-icon.minus:hover {
  background: var(--gray-300);
}
```

### 4.2 商品卡片

```css
.product-card {
  background: var(--white);
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  transition: transform 0.2s ease, box-shadow 0.2s ease;
}
.product-card:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.08);
}
.product-card:active {
  transform: translateY(0);
}
.product-card .image {
  width: 100%;
  aspect-ratio: 1;
  object-fit: cover;
  background: var(--gray-100);
}
.product-card .info {
  padding: 10px 12px 12px;
}
.product-card .name {
  font-size: 14px;
  font-weight: 600;
  color: var(--gray-900);
  line-height: 1.4;
  margin-bottom: 4px;
  /* 最多2行截断 */
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.product-card .desc {
  font-size: 11px;
  color: var(--gray-500);
  line-height: 1.4;
  margin-bottom: 8px;
  display: -webkit-box;
  -webkit-line-clamp: 1;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
.product-card .price-row {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.product-card .price {
  font-family: var(--font-number);
  font-size: 18px;
  font-weight: 700;
  color: var(--gray-900);
}
.product-card .price .yen {
  font-size: 12px;
  font-weight: 600;
}
```

### 4.3 分类导航

```css
.category-nav {
  display: flex;
  gap: 0;
  overflow-x: auto;
  scrollbar-width: none;
  -ms-overflow-style: none;
  background: var(--white);
  border-bottom: 1px solid var(--gray-200);
  position: sticky;
  top: 0;
  z-index: 10;
}
.category-nav::-webkit-scrollbar { display: none; }
.category-tab {
  flex-shrink: 0;
  padding: 12px 18px;
  font-size: 14px;
  font-weight: 400;
  color: var(--gray-600);
  background: none;
  border: none;
  cursor: pointer;
  position: relative;
  transition: color 0.2s ease;
  white-space: nowrap;
}
.category-tab:hover {
  color: var(--gray-900);
}
.category-tab.active {
  color: var(--heytea-green);
  font-weight: 600;
}
.category-tab.active::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 24px;
  height: 3px;
  background: var(--heytea-green);
  border-radius: 2px;
}
```

### 4.4 购物车底栏

```css
.cart-bar {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  height: 56px;
  background: var(--gray-900);
  display: flex;
  align-items: center;
  padding: 0 16px;
  z-index: 100;
  box-shadow: 0 -2px 12px rgba(0, 0, 0, 0.1);
}
.cart-bar .cart-icon-wrap {
  position: relative;
  width: 44px;
  height: 44px;
  background: var(--gray-700);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: -12px;
  border: 3px solid var(--gray-900);
}
.cart-bar .cart-icon-wrap.has-items {
  background: var(--heytea-green);
}
.cart-bar .badge {
  position: absolute;
  top: -4px;
  right: -4px;
  min-width: 18px;
  height: 18px;
  background: var(--red);
  color: var(--white);
  font-size: 11px;
  font-weight: 600;
  border-radius: 9px;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 4px;
}
.cart-bar .total-price {
  flex: 1;
  margin-left: 12px;
  color: var(--white);
  font-family: var(--font-number);
  font-size: 20px;
  font-weight: 700;
}
.cart-bar .total-price .yen {
  font-size: 13px;
  font-weight: 600;
}
.cart-bar .delivery-tip {
  font-size: 11px;
  color: var(--gray-500);
  margin-left: 4px;
}
.cart-bar .checkout-btn {
  background: var(--heytea-green);
  color: var(--white);
  border: none;
  border-radius: 20px;
  padding: 8px 20px;
  font-size: 14px;
  font-weight: 600;
  cursor: pointer;
  transition: background 0.2s ease;
}
.cart-bar .checkout-btn:hover {
  background: var(--heytea-green-dark);
}
.cart-bar .checkout-btn:disabled {
  background: var(--gray-600);
  cursor: not-allowed;
}
```

### 4.5 商品详情弹窗

```css
.modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
  z-index: 200;
  display: flex;
  align-items: flex-end;
  justify-content: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
}
.modal-overlay.open {
  opacity: 1;
  pointer-events: auto;
}
.modal-sheet {
  background: var(--white);
  border-radius: 20px 20px 0 0;
  width: 100%;
  max-width: 480px;
  max-height: 85vh;
  overflow-y: auto;
  transform: translateY(100%);
  transition: transform 0.35s cubic-bezier(0.32, 0.72, 0, 1);
}
.modal-overlay.open .modal-sheet {
  transform: translateY(0);
}
```

### 4.6 标签 / Tag

```css
.tag {
  display: inline-flex;
  align-items: center;
  padding: 2px 8px;
  border-radius: 4px;
  font-size: 11px;
  font-weight: 500;
  line-height: 1.4;
}
.tag-hot {
  background: rgba(var(--red-rgb), 0.1);
  color: var(--red);
}
.tag-new {
  background: rgba(var(--heytea-green-rgb), 0.1);
  color: var(--heytea-green);
}
.tag-season {
  background: rgba(var(--orange-rgb), 0.1);
  color: var(--orange);
}
```

### 4.7 导航栏

```css
.navbar {
  height: 52px;
  background: var(--white);
  display: flex;
  align-items: center;
  justify-content: center;
  position: sticky;
  top: 0;
  z-index: 50;
  border-bottom: 1px solid var(--gray-200);
}
.navbar .title {
  font-size: 17px;
  font-weight: 600;
  color: var(--gray-900);
}
.navbar .back-btn {
  position: absolute;
  left: 12px;
  width: 36px;
  height: 36px;
  display: flex;
  align-items: center;
  justify-content: center;
  border: none;
  background: none;
  cursor: pointer;
  border-radius: 50%;
  transition: background 0.15s ease;
}
.navbar .back-btn:hover {
  background: var(--gray-100);
}
```

---

## 5. Layout Principles

**容器**：
- 移动端优先，最大宽度 480px 居中
- 桌面端显示手机模拟器外壳

**网格**：
- 商品列表：2列网格，gap 10px
- 首页功能入口：4列网格

**间距梯度**：
```css
--space-xs: 4px;
--space-sm: 8px;
--space-md: 12px;
--space-lg: 16px;
--space-xl: 20px;
--space-2xl: 24px;
--space-3xl: 32px;
```

**安全距离**：
- 页面左右边距：16px
- 卡片内边距：12px
- 底部安全区：购物车高度 56px + 安全区 20px

---

## 6. Depth & Elevation

```css
--shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.04);
--shadow-md: 0 4px 12px rgba(0, 0, 0, 0.06);
--shadow-lg: 0 8px 24px rgba(0, 0, 0, 0.08);
--shadow-xl: 0 16px 48px rgba(0, 0, 0, 0.12);
--shadow-cart: 0 -2px 12px rgba(0, 0, 0, 0.1);
```

---

## 7. Animation & Interaction

**交互档位：L2 流畅交互**

### 7.1 入场动画
```css
/* 淡入上移 */
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(16px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}
.animate-fade-in-up {
  animation: fadeInUp 0.5s ease forwards;
  opacity: 0;
}

/* Stagger 延迟 */
.stagger-1 { animation-delay: 0.05s; }
.stagger-2 { animation-delay: 0.1s; }
.stagger-3 { animation-delay: 0.15s; }
.stagger-4 { animation-delay: 0.2s; }
```

### 7.2 滚动 Reveal
```css
.reveal {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease, transform 0.6s ease;
}
.reveal.visible {
  opacity: 1;
  transform: translateY(0);
}
```

### 7.3 购物车弹跳
```css
@keyframes cartBounce {
  0% { transform: scale(1); }
  30% { transform: scale(1.2); }
  50% { transform: scale(0.95); }
  70% { transform: scale(1.05); }
  100% { transform: scale(1); }
}
.cart-bounce {
  animation: cartBounce 0.4s ease;
}
```

### 7.4 飞入购物车动画
```css
@keyframes flyToCart {
  0% {
    opacity: 1;
    transform: translate(0, 0) scale(1);
  }
  100% {
    opacity: 0;
    transform: translate(var(--fly-x), var(--fly-y)) scale(0.3);
  }
}
```

### 7.5 Banner 自动轮播
```css
@keyframes slideIn {
  from { transform: translateX(100%); opacity: 0; }
  to { transform: translateX(0); opacity: 1; }
}
@keyframes slideOut {
  from { transform: translateX(0); opacity: 1; }
  to { transform: translateX(-100%); opacity: 0; }
}
```

### 7.6 prefers-reduced-motion
```css
@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

---

## 8. Do's and Don'ts

### ✅ Do's
1. **所有颜色通过 CSS 变量引用**，零硬编码
2. **图片使用 Unsplash 真实饮品图**，禁止纯色块占位
3. **中文字体优先**，font-family 链中 PingFang SC / Noto Sans SC 在前
4. **行高 ≥ 1.6**，正文 ≥ 14px，保证中文可读性
5. **触摸目标 ≥ 44×44px**，符合移动端操作规范
6. **购物车状态实时同步**，数量变化有动画反馈
7. **商品卡片 hover 有微交互**（上浮 + 阴影）
8. **分类切换有平滑过渡**，active 态有下划线指示器

### ❌ Don'ts
1. **禁止使用 Emoji** 作为图标或装饰元素
2. **禁止纯色块占位图**，必须使用真实图片
3. **禁止移动端横向溢出**，所有内容在 375px 内完整展示
4. **禁止使用 filter: blur()** 在滚动元素上
5. **禁止超过 3 种标签颜色**，保持视觉统一
6. **禁止使用 alert() / confirm()**，用 toast 或弹窗替代
7. **禁止在暗色背景上使用低对比度文字**
8. **禁止无动画的页面切换**，至少有 fade 过渡
9. **禁止购物车为空时显示结算按钮**（应 disabled）
10. **禁止商品价格使用非数字字体**

---

## 9. Responsive Behavior

**断点**：
```css
/* 移动端（默认） */
@media (max-width: 480px) { /* 基础样式 */ }

/* 平板 */
@media (min-width: 481px) and (max-width: 768px) {
  /* 容器居中，最大宽度 480px */
}

/* 桌面端 */
@media (min-width: 769px) {
  /* 显示手机模拟器外壳，居中展示 */
}
```

**触摸目标**：
- 所有可点击元素最小 44×44px
- 分类标签 padding 确保触摸区域足够
- 加购按钮直径 ≥ 28px

**折叠策略**：
- 移动端：单列/双列自适应
- 桌面端：固定 480px 宽度手机模拟器

**安全区域**：
```css
padding-bottom: calc(56px + env(safe-area-inset-bottom, 20px));
```
