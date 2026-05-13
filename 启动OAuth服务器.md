# 知乎 OAuth 服务器启动指南

## 🚀 快速启动

### 步骤1：检查 Node.js 环境
打开命令行窗口，运行：
```powershell
node --version
```
如果显示版本号（如 v18.x.x），说明已安装 Node.js。

### 步骤2：启动 OAuth 服务器
```powershell
cd "E:\Trae SOLO\知乎 Hackathon  AI 脑洞实验室"
node zhihu-oauth-server.js
```

### 步骤3：访问授权页面
打开浏览器访问：
```
http://localhost:17993
```

### 步骤4：开始授权
1. 确认 APP_ID 和 APP_KEY 已填写（默认已配置）
2. 点击「使用知乎账号登录」
3. 在知乎授权页面完成登录和授权
4. 授权成功后自动跳转到个人详情页

---

## 📋 服务器功能

### 已实现的功能
✅ OAuth 2.0 授权流程
✅ 安全的后端 token 交换
✅ 用户信息获取
✅ CSRF 防护
✅ 本地 token 存储

### API 端点
- `GET /` - 首页表单
- `GET /api/auth/zhihu/url` - 生成授权 URL
- `GET /callback` - OAuth 回调处理
- `POST /api/auth/zhihu/callback` - 后端交换 token
- `GET /profile?token=xxx` - 用户详情页
- `GET /api/user` - 代理用户信息 API

---

## 🔐 配置说明

### 当前配置
- **APP_ID**: `Limomei-90-12-3`
- **APP_KEY**: `P1DzGVNzXIftS10Oc644qrxGotj4wtt7`
- **回调地址**: `http://localhost:17993/callback`
- **监听端口**: `17993`

### 修改配置
如果需要修改配置，可以：
1. 直接编辑 `zhihu-oauth-server.js`
2. 或者在启动后的网页表单中修改

---

## ⚠️ 重要提示

### 安全性
- APP_KEY 只在本地使用，不会发送到浏览器
- Token 存储在服务器内存中
- 使用 CSRF 防护

### 跨域问题
- 本地服务器解决了浏览器跨域问题
- 所有 API 请求通过服务器代理

### 部署注意
- 仅供本地开发和测试使用
- 生产环境需要更强的安全措施
- Token 存储需要使用数据库

---

## 🎯 使用流程

```
用户浏览器
    ↓
http://localhost:17993 (首页表单)
    ↓ 点击登录
知乎授权页面
    ↓ 授权成功
/callback (处理授权码)
    ↓ POST
/api/auth/zhihu/callback (后端换token)
    ↓
知乎 API (获取 access_token)
    ↓
/profile?token=xxx (显示用户信息)
```

---

## 💡 常见问题

### Q: 授权页面打不开？
A: 确保服务器已启动，端口 17993 未被占用

### Q: 授权失败？
A: 检查 APP_ID 和 APP_KEY 是否正确

### Q: Token 过期？
A: 需要重新授权登录

### Q: 端口被占用？
A: 修改 zhihu-oauth-server.js 中的 PORT 常量

---

## 🔧 调试

服务器会在控制台输出：
- `[CURL]` - 模拟的 curl 命令
- `[AUTH]` - 授权 URL 生成信息
- `[RES]` - API 响应数据

---

**提示**：服务器启动后会显示"OAuth 演示服务已启动"，表示服务正常运行！
