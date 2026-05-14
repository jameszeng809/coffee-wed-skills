---
name: Coffee-Wed-Skills
version: "1.0"
description: >
  一键生成咖啡品牌全栈电商网站。输入品牌名称、主题色、产品列表即可自动输出
  完整单文件 HTML（含登录注册、购物车、模拟支付、订单确认），直接部署到
  EdgeOne Pages 无需任何后端服务。专为 WorkBuddy Skill 比赛设计，最省积分方案。
author: WorkBuddy User
agent_created: true
tags:
  - coffee
  - ecommerce
  - web-generation
  - edgeone
  - fullstack
trigger_phrases:
  - 生成咖啡网站
  - 创建咖啡电商
  - 帮我做咖啡网页
  - coffee website
  - generate coffee shop
---

# Coffee-Wed-Skills

## 用途

根据用户提供的咖啡品牌信息，**一次性生成完整的单文件全栈网站 HTML**。生成的网站包含：

- 首页（Banner + 品牌介绍 + 精选产品）
- 产品列表页（分类筛选、价格展示）
- 购物车（前端状态管理，支持增减、删除）
- 用户登录 / 注册（浏览器本地存储，无需后端）
- 模拟支付流程（微信/支付宝 UI 风格弹窗 → 订单成功页）
- 响应式设计（PC + 移动端兼容）

## 使用方法

直接告诉我以下信息（不提供则使用默认值）：

| 参数 | 说明 | 默认值 |
|------|------|-------|
| `品牌名称` | 咖啡网站的名称 | Bean Journey Coffee |
| `品牌副标题` | 一句话品牌描述 | 每一杯，都是一段旅程 |
| `主题色` | 主色调（十六进制或颜色名） | #6B4226（咖啡棕） |
| `辅助色` | 强调色 | #D4A96A（焦糖金） |
| `产品列表` | 产品名称和价格（逗号分隔） | 默认6款咖啡产品 |
| `货币` | 显示货币符号 | ¥（人民币） |
| `语言` | 页面语言 | 中文 |

## 执行步骤

收到用户请求后，按以下步骤执行：

### Step 1：解析参数

从用户输入中提取上表中的参数，缺失的使用默认值填充。将产品列表整理成结构化数组（名称、价格、描述、分类）。

### Step 2：生成网站 HTML

生成一个完整的 `index.html` 文件，必须包含以下所有功能模块：

#### 2.1 技术规范
- 使用 Tailwind CSS（CDN：`https://cdn.tailwindcss.com`）
- 使用原生 JavaScript（无框架依赖）
- 所有数据用 JS 对象/数组硬编码在 `<script>` 标签内
- 用户数据用 `localStorage` 持久化（键名：`cwb_users`、`cwb_current_user`、`cwb_cart`）
- 单个 `index.html` 文件，不依赖任何外部文件

#### 2.2 页面结构
```
<nav>      导航栏：Logo + 菜单 + 购物车图标（带数量徽标）+ 登录状态
<section>  Hero Banner：全宽大图背景色 + 品牌名 + CTA 按钮
<section>  精选产品：6张产品卡片，带"加入购物车"按钮
<section>  品牌故事：可持续/公平贸易主题文案
<footer>   页脚：联系方式 + 版权
<div>      购物车侧边栏（滑出式 Drawer）
<div>      登录/注册模态框（Tab 切换）
<div>      支付模态框（微信/支付宝/银行卡三种方式 Tab）
<div>      订单成功页（覆盖层，含订单号）
```

#### 2.3 功能实现规范

**登录/注册（零后端）**
```javascript
// 注册：将用户存入 localStorage
function register(username, password) {
  const users = JSON.parse(localStorage.getItem('cwb_users') || '[]');
  // 检查用户名是否已存在
  // 存储时对密码做简单哈希（btoa）
  // 写回 localStorage
}

// 登录：验证后写入 currentUser
function login(username, password) {
  // 从 localStorage 读取用户列表验证
  // 成功则设置 cwb_current_user
  // 更新导航栏显示用户名
}
```

**购物车（前端状态）**
```javascript
// 购物车数据结构
let cart = JSON.parse(localStorage.getItem('cwb_cart') || '[]');
// { id, name, price, qty, image }

function addToCart(productId) { /* 已有则+1，没有则push */ }
function updateQty(productId, delta) { /* 最小为1，0则removeFromCart */ }
function removeFromCart(productId) { /* 过滤掉该item */ }
function getCartTotal() { /* 求和 */ }
// 每次操作后调用 saveCart() + renderCart() + updateBadge()
```

**模拟支付**
```javascript
function showPayment() {
  // 展示支付模态框
  // Tab 切换：微信支付（二维码占位图）/ 支付宝（二维码占位图）/ 银行卡（卡号表单）
  // 点击"确认支付"：生成随机订单号（8位），清空购物车，显示订单成功页
}
```

#### 2.4 视觉风格要求
- 整体风格：温暖、精品咖啡馆调性
- 使用品牌主题色和辅助色定义 Tailwind 自定义颜色
- 产品卡片：圆角、阴影、悬停放大效果
- 按钮：主色背景、白色文字，悬停变深
- 字体：使用 Google Fonts（Noto Sans SC / Playfair Display）

### Step 3：写入文件

将生成的 HTML 内容写入工作区的 `index.html` 文件。

### Step 4：预览

调用 `preview_url` 工具，传入 `index.html` 的绝对路径，为用户展示网站效果。

### Step 5：部署提示

告知用户如何通过 EdgeOne Pages Skill 部署上线，提供步骤说明。

## 输出格式

执行完成后，输出：
1. 已生成的网站功能清单（已实现 / 未实现）
2. `index.html` 文件路径
3. 预览链接
4. EdgeOne 部署指引

## 注意事项

- 生成时务必保证 HTML 文件完整可运行，不要留任何占位符（`TODO`、`...`）
- 支付功能是模拟演示，不接入真实支付网关，但 UI 要逼真
- 登录功能使用浏览器本地存储，提交比赛时需在 README 中说明这是 Demo 模式
- 产品图片使用 `https://via.placeholder.com` 占位，或使用咖啡相关 Unsplash 图片 URL

## 示例对话

**用户：** 帮我生成一个咖啡网站

**助手：** 好的，我将使用默认品牌「Bean Journey Coffee」为你生成完整电商网站，包含登录、购物车和支付功能……（执行步骤1-5）

---

**用户：** 生成一个叫「晨露咖啡」的网站，主题色用深绿色，卖手冲咖啡豆、挂耳咖啡、冷萃液，价格分别是¥128、¥68、¥158

**助手：** 收到，品牌「晨露咖啡」，深绿主题……（执行步骤1-5）
