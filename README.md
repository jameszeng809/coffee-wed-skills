# Coffee-Wed-Skills

> WorkBuddy Skill 比赛参赛作品
> 
> **一句话描述**：输入咖啡品牌信息，自动生成带登录、购物车、支付的全栈电商网站，一键部署到 EdgeOne Pages。

---

## 功能特性

| 功能 | 实现方式 | 说明 |
|------|---------|------|
| 用户登录/注册 | 浏览器本地存储 | Demo 模式，无需后端，数据存储在访问者本地 |
| 购物车 | 前端 JS 状态管理 | 支持加购、调整数量、删除，刷新不丢失 |
| 模拟支付 | 沙盒 UI 弹窗 | 微信/支付宝/银行卡三种方式，点击确认生成订单号 |
| 产品展示 | 静态 JSON 数据 | 6款精选咖啡，支持自定义产品列表 |
| 响应式设计 | Tailwind CSS CDN | 适配 PC 和移动端 |

## 文件结构

```
Coffee-Wed-Skills/
├── SKILL.md          ← WorkBuddy Skill 核心定义文件（参赛主文件）
├── index.html        ← SKILL 生成的示例网站（可直接部署）
├── README.md         ← 本文件（使用说明）
└── preview/          ← （可选）截图预览
```

## 如何使用此 SKILL

### 方式一：在 WorkBuddy 中直接调用

安装后，在 WorkBuddy 对话框输入：

```
生成咖啡网站
```

或带参数：

```
帮我生成一个叫「晨露咖啡」的网站，主题色用深绿色，
卖手冲咖啡豆（¥128）、挂耳咖啡（¥68）、冷萃液（¥158）
```

### 方式二：直接使用示例文件

将 `index.html` 上传到 EdgeOne Pages 即可访问演示网站。

## 部署到 EdgeOne Pages

1. 打开 WorkBuddy，连接 `edgeone-pages` Connector
2. 告诉 WorkBuddy：「把 Desktop/Coffee-Wed-Skills/index.html 部署到 EdgeOne Pages」
3. 获取公网访问链接，分享给任何人

## 技术说明

- **零后端依赖**：登录数据存储在用户浏览器 `localStorage`，刷新页面保持登录状态
- **支付为演示模式**：支付界面完整还原微信/支付宝风格，但不连接真实支付网关
- **单文件部署**：整个网站是一个 `index.html`，无需 npm install 或构建步骤

## 许可证

本作品用于 WorkBuddy Skill 开发比赛，遵循比赛规则。

---

*由 WorkBuddy Coffee-Wed-Skills 生成 · 2026*
