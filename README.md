# 客户端

## 项目概述

本项目是一个基于 Vue 3 和 axios 构建的前端项目，用于 RM 后端项目(https://github.com/Aplaoi/remote-backend)的可视化展示，需要在 Node.js 环境下运行。项目使用 Vite 作为构建工具，Element Plus 作为 UI 组件库。

## 项目运行

项目建议使用 vscode 或者 WebStorm 等 IDE 打开

### 安装 Node.js

从 Node.js 官方网站（https://nodejs.org/）下载并安装

### 安装项目依赖

在项目根目录下，使用 npm 安装相关依赖：

```bash
npm install vue@latest
npm install axios
npm install element-plus
```

### 修改后端地址

在`App.vue`的第8行处将地址修改为服务端的静态ip地址，注意**格式**

```javascript
const url = "http://192.168.0.105:9002";
```

### 运行项目

在项目根目录下，运行以下命令启动开发服务器：

```bash
npm run dev
```

运行命令后，按照控制台的提示内容打开相关网页 (例如`http://localhost:5173`) 进行访问即可。
