# Stuff Happens - 网页卡牌游戏

## 项目简介
"Stuff Happens" 是一个基于 React + Node.js 的单页网页应用，实现了一款有趣的卡牌排序游戏。玩家需要根据描述判断新抽到的"不幸事件"卡牌在其已有卡牌中的"不幸指数"排序位置。

## 技术栈
- **前端**: React, React Router, React Bootstrap
- **后端**: Node.js, Express, Passport.js
- **数据库**: SQLite
- **认证**: Session-based 认证

## 安装与运行

### 前置要求
- Node.js 22.x LTS
- npm
- nodemon (全局安装)

### 启动命令
```bash
# 启动后端服务器
cd server
npm install
nodemon index.mjs

# 启动前端开发服务器
cd client
npm install
npm run dev
```

## 服务器端 API 接口

### 认证相关
- `POST /api/sessions` - 用户登录
- `DELETE /api/sessions/current` - 用户登出
- `GET /api/sessions/current` - 获取当前用户信息

### 游戏相关
- `GET /api/cards` - 获取所有卡牌列表
- `POST /api/games` - 开始新游戏
- `GET /api/games/current` - 获取当前游戏状态
- `PUT /api/games/current` - 提交游戏回合
- `DELETE /api/games/current` - 结束当前游戏

### 用户相关
- `GET /api/users/current/history` - 获取用户游戏历史

## 数据库表结构

### users 表
存储用户认证信息
- id (主键)
- username (用户名)
- password (加密密码)
- salt (密码盐值)

### cards 表
存储卡牌信息
- id (主键)
- name (情境名称)
- image (图片URL)
- bad_luck_index (不幸指数)

### games 表
存储游戏记录
- id (主键)
- user_id (用户ID)
- outcome (游戏结果)
- start_time (开始时间)
- end_time (结束时间)

### game_cards 表
游戏与卡牌的关联表
- game_id (游戏ID)
- card_id (卡牌ID)
- round (获取回合)
- won (是否获胜获得)

## 客户端路由

### 路由配置
- `/` - 首页，显示游戏介绍和登录入口
- `/login` - 用户登录页面
- `/game` - 游戏主界面
- `/profile` - 用户个人信息和历史记录
- `/demo` - 匿名用户演示游戏

## 主要 React 组件

### 布局组件
- `App` - 根组件，处理路由和认证状态
- `Navigation` - 导航栏组件
- `Layout` - 页面布局容器

### 页面组件
- `Home` - 首页组件
- `Login` - 登录表单组件
- `Profile` - 用户档案和历史记录
- `Game` - 游戏主界面组件
- `DemoGame` - 演示游戏组件

### 游戏组件
- `Card` - 卡牌展示组件
- `GameBoard` - 游戏面板组件
- `RoundResult` - 回合结果展示
- `GameSummary` - 游戏总结

### 通用组件
- `Loading` - 加载状态组件
- `Message` - 消息提示组件

## 应用截图

### 游戏界面
![游戏界面](./screenshots/game.png)

### 用户历史记录
![历史记录](./screenshots/history.png)

## 测试账户

| 用户名 | 密码 |
|--------|------|
| demo | demo |
| bob | bob123 |

## 游戏规则
1. 游戏开始时玩家获得3张随机卡牌
2. 每轮展示一张新卡牌（仅名称和图片）
3. 玩家需在30秒内判断新卡牌在已有卡牌中的排序位置
4. 猜对则获得该卡牌，猜错或超时则失败一次
5. 收集满6张卡牌获胜，失败3次则游戏结束

## 开发说明
- 项目采用严格的 SPA 架构，前后端分离
- 使用 React Hooks 进行状态管理
- 所有API请求都经过认证保护
- 数据库预加载至少50张主题卡牌

## 许可证
MIT License
