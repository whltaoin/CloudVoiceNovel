# Capacitor 打包 iOS 步骤、App Store 发布

## 前提条件

### 开发环境
- macOS 系统
- Xcode 13.0 或更高版本
- Node.js 16.x 或更高版本
- CocoaPods

### 开发者账号
- Apple Developer Program 账号（付费订阅）
- 已配置证书和描述文件

## Capacitor 配置

### 安装 Capacitor
```bash
# 在项目根目录执行
npm install @capacitor/core @capacitor/cli
npx cap init [AppName] [BundleID]
```

### 添加 iOS 平台
```bash
npm install @capacitor/ios
npx cap add ios
```

### 配置 app.json
确保 `capacitor.config.json` 包含以下信息：
```json
{
  "appId": "com.yourcompany.cloudvoicenovel",
  "appName": "CloudVoiceNovel",
  "webDir": "build",
  "bundledWebRuntime": false,
  "plugins": {
    "SplashScreen": {
      "launchShowDuration": 0
    }
  }
}
```

## iOS 构建步骤

### 1. 构建 Web 资源
```bash
npm run build
npx cap sync ios
```

### 2. 打开 Xcode 项目
```bash
npx cap open ios
```

### 3. 配置证书和描述文件
在 Xcode 中：
- 选择项目 -> 点击项目名称 -> 选择 "Signing & Capabilities"
- 选择你的团队
- 确保 "Automatically manage signing" 已勾选
- 选择适当的 Provisioning Profile

### 4. 配置应用信息
- 更新应用图标和启动画面
- 修改 Display Name
- 设置版本号和构建号

### 5. 构建应用
- 选择目标设备（Generic iOS Device 或真机）
- 点击 Product -> Archive

### 6. 上传到 App Store Connect
- 构建完成后，会自动打开 Organizer
- 选择构建版本 -> 点击 "Distribute App"
- 选择 "App Store Connect" -> 点击 "Next"
- 选择 "Upload" -> 点击 "Next"
- 确认选项 -> 点击 "Upload"

## App Store 发布流程

### 1. 准备 App Store Connect
- 登录 [App Store Connect](https://appstoreconnect.apple.com/)
- 创建新的 App（如果尚未创建）
- 填写应用信息：名称、描述、关键词、支持 URL 等

### 2. 上传应用截图和预览
- 准备不同尺寸的应用截图
- 可选：添加应用预览视频

### 3. 设置应用定价和销售范围
- 选择应用的价格等级
- 设置可销售的国家和地区

### 4. 提交审核
- 在 App Store Connect 中，点击 "+" 版本或平台
- 填写版本信息、新增功能描述
- 选择已上传的构建版本
- 回答内容审核问题
- 点击 "提交审核"

### 5. 审核跟踪
- 应用将进入 "等待审核" 状态
- 审核过程中可能需要提供额外信息
- 审核通过后，应用将自动发布或等待您手动发布

## 常见问题解决

### 证书和描述文件问题
- 确保开发者账号有效
- 检查证书是否过期
- 确认设备 UDID 是否已添加到开发者账号

### 构建错误
- 检查依赖项版本兼容性
- 查看 Xcode 错误日志
- 确保所有插件兼容 iOS 最新版本

### App Store 审核被拒
- 确保遵循 App Store 审核指南
- 提供明确的应用功能描述
- 确保所有权限请求都有合理说明

## 自动化构建配置（可选）

### 使用 Fastlane
```bash
# 安装 Fastlane
gem install fastlane

# 在 iOS 目录初始化 Fastlane
cd ios
fastlane init
```

### 配置 CI/CD
可以使用 GitHub Actions、Jenkins 等工具配置自动化构建和发布流程。