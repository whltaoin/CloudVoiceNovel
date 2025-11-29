# 在线接口调试地址（后端启动后访问）

## Swagger 接口文档访问说明

### 本地开发环境

#### 启动后端服务后，通过以下地址访问 Swagger 文档：
- **Swagger UI**: http://localhost:3000/api/docs
- **OpenAPI JSON**: http://localhost:3000/api/docs-json

### 测试环境

#### 测试环境 Swagger 文档地址：
- **Swagger UI**: http://test-api.cloudvoicenovel.com/api/docs
- **OpenAPI JSON**: http://test-api.cloudvoicenovel.com/api/docs-json

### 生产环境

> **注意**：生产环境的 Swagger 文档默认不对外开放，如需访问请联系系统管理员开启临时权限。

## Swagger 使用指南

### 基本功能

1. **接口浏览**：查看所有已定义的 API 接口列表
2. **接口详情**：查看每个接口的 URL、方法、请求参数、返回结果等详细信息
3. **在线调试**：直接在浏览器中发送请求并查看响应结果
4. **认证设置**：设置认证信息（如 JWT Token）以访问需要授权的接口

### 使用步骤

#### 1. 访问 Swagger UI 页面
打开浏览器，输入对应的 Swagger UI 地址。

#### 2. 身份认证（如需）
- 点击右上角的 "Authorize" 按钮
- 在弹出的对话框中，选择合适的认证方式
- 对于 JWT 认证，在输入框中输入 `Bearer {token}` 格式的令牌
- 点击 "Authorize" 完成认证设置

#### 3. 接口调试
- 选择需要测试的接口
- 点击 "Try it out" 按钮
- 填写必要的请求参数
- 点击 "Execute" 发送请求
- 在下方查看请求响应结果

## 注意事项

1. **环境区分**：确保使用的是正确环境的 Swagger 地址
2. **认证信息**：敏感接口需要先进行身份认证
3. **参数验证**：填写参数时请遵循接口文档中的格式要求
4. **请求限制**：为保证系统稳定性，请勿频繁发送大量请求
5. **安全提示**：请勿在公共网络环境下暴露认证信息

## 常见问题

### Q: 访问 Swagger 页面显示 404？
A: 确认后端服务是否正常启动，以及 Swagger 中间件是否正确配置。

### Q: 调用需要认证的接口失败？
A: 检查是否已正确设置认证信息，Token 是否有效。

### Q: 接口响应错误？
A: 仔细检查请求参数是否符合要求，或联系后端开发人员排查问题。

## 联系方式

如在使用 Swagger 过程中遇到问题，请联系：
- 技术支持邮箱：support@cloudvoicenovel.com
- 技术交流群：[扫码加入](https://example.com/tech-group)