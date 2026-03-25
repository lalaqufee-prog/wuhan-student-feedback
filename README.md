# 江城少年每日反馈站

一个面向中国武汉初中生的 Vue 前端网站，用来反馈每天的学习内容、作业内容、作业完成情况、学校活动和有趣的事情。

## 功能简介

- 记录今日学习内容
- 记录今日作业内容
- 用滑块反馈作业完成度
- 记录校园活动和有趣瞬间
- 实时预览今日反馈卡

## 本地开发

先确保已经安装 Node.js。

```bash
npm install
npm run dev
```

本地启动后，默认可在浏览器打开：

```text
http://localhost:5173
```

## 打包构建

```bash
npm run build
```

构建完成后，产物会输出到 `dist` 目录。

## 部署到 Vercel

1. 把本项目上传到 GitHub 仓库
2. 登录 Vercel
3. 导入 GitHub 仓库
4. 确认以下配置：

- Framework Preset: `Vite`
- Install Command: `npm install`
- Build Command: `npm run build`
- Output Directory: `dist`

5. 点击 Deploy，等待生成线上地址

## 项目结构

```text
.
├─ index.html
├─ package.json
├─ vite.config.js
└─ src
   ├─ App.vue
   ├─ main.js
   └─ styles.css
```
