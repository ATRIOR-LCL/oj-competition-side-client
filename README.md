# SDUT OJ 竞赛客户端

SDUT OJ 竞赛客户端是一个基于 Electron 的专业在线评测系统客户端应用程序，专为 SDUT ACM 算法竞赛环境设计，提供安全、稳定、功能完整的比赛环境。

## 🏆 核心特性

### 🛡️ 高级安全控制
- **� 智能域名拦截** - 内置白名单/黑名单机制，智能拦截非法域名访问
- **🚫 重定向拦截** - 自动检测并拦截恶意重定向，智能回退到安全域名
- **🔄 智能回退逻辑** - 重定向拦截后自动回退到重定向前的顶级域名，保护比赛环境
- **🎯 弹窗拦截管理** - 完善的新窗口拦截系统，支持白名单域名的安全访问
- **💬 友好拦截提示** - 可爱的随机化拦截提示，提升用户体验

### 🎨 现代化界面
- **🔧 独立工具栏** - 基于 BrowserView 的独立工具栏，支持后退、前进、刷新、主页、系统信息等完整操作
- **🖱️ 智能按钮状态** - 工具栏按钮根据页面状态智能启用/禁用（如后退/前进按钮）
- **🎨 主题自适应** - 本地 SVG 图标，完美支持系统亮色/暗色主题自动切换
- **📱 响应式设计** - 适配不同屏幕尺寸，提供一致的用户体验

### ⌨️ 全平台快捷键
- **🌍 跨平台支持** - Windows、macOS、Linux 全平台快捷键支持，操作体验统一
- **🍎 macOS 原生菜单** - macOS 下使用原生应用菜单，支持系统快捷键
- **⚡ 智能焦点检测** - 自动检测输入框焦点，避免快捷键冲突
- **🔄 动态更新** - 快捷键状态实时更新，确保功能准确性

### 🪟 智能窗口管理
- **📋 完整工具栏** - 新窗口自动创建完整的导航工具栏
- **🔗 外部链接支持** - 支持排行榜等白名单外部链接的安全访问
- **🎯 主页跳转优化** - 智能主页跳转，确保始终返回正确的初始URL
- **🔄 URL 状态管理** - 动态更新窗口初始URL，避免重定向循环

### 🛡️ 开发者工具防护
- **🚫 全面禁用** - 彻底禁用开发者工具和调试功能，确保比赛公平性
- **⌨️ 快捷键拦截** - 拦截所有开发者工具相关快捷键
- **🔒 右键菜单控制** - 恢复系统默认右键菜单行为，移除开发者选项

### 🌍 多平台架构支持
- **💻 全架构构建** - 支持 x64 和 arm64 架构（Windows、macOS、Linux）
- **� 多格式输出** - Windows (NSIS/Portable)、macOS (DMG/ZIP)、Linux (AppImage/DEB)
- **� 平台优化** - 针对不同平台的特定优化和兼容性处理

## 🚀 系统要求

- **操作系统**: Windows 10+、macOS 10.14+、Linux (Ubuntu 18.04+)
- **Node.js**: 16.0.0 或更高版本
- **架构支持**: x64、arm64
- **内存**: 建议 4GB RAM 或以上
- **存储**: 至少 200MB 可用磁盘空间
- **网络**: 稳定的互联网连接

## 📦 安装和运行

### 快速开始

1. **克隆项目**
   ```bash
   git clone https://github.com/ATRIOR-LCL/oj-competition-side-client.git
   cd oj-competition-side-client
   ```

2. **安装依赖**
   ```bash
   npm install
   ```

3. **启动应用**
   ```bash
   npm start
   ```

### 构建发布版本

```bash
# 构建所有平台版本
npm run build

# 构建特定平台
npm run build:win    # Windows 版本
npm run build:mac    # macOS 版本  
npm run build:linux  # Linux 版本
```

## ⌨️ 快捷键支持

| 功能 | Windows/Linux | macOS | 说明 |
|------|---------------|-------|------|
| 后退 | Alt + ← | Cmd + ← | 返回上一页 |
| 前进 | Alt + → | Cmd + → | 前进到下一页 |
| 刷新 | F5 / Ctrl + R | Cmd + R | 刷新当前页面 |
| 主页 | Alt + H | Cmd + Shift + H | 返回窗口初始页面 |
| 系统信息 | Alt + I | Cmd + I | 显示系统信息弹窗 |

> � **智能焦点检测**: 当焦点在输入框时，快捷键会自动让位给系统默认行为，避免冲突。

## 🔒 安全特性详解

### 域名控制系统
- **主域名**: `op.sdutacm.cn` - 主窗口允许访问的根域名
- **白名单域名**: 
  - `rl.algoux.cn` - 算法竞赛相关
  - `rl.algoux.org` - 算法竞赛相关  
  - `rank.ac` - 排行榜系统
  - `acm.sdut.edu.cn` - SDUT ACM 官网
- **黑名单域名**: `oj.sdutacm.cn` - 明确禁止访问

### 重定向拦截机制
- **实时监控**: 监听页面重定向行为
- **智能拦截**: 自动拦截非法重定向目标
- **安全回退**: 回退到重定向前的顶级域名，而非系统主域名
- **URL 更新**: 动态更新窗口初始URL，避免循环重定向

### 弹窗管理系统
- **白名单弹窗**: 允许白名单域名在新窗口安全打开
- **完整工具栏**: 新窗口自动创建完整的导航系统
- **安全拦截**: 非白名单域名弹窗会被拦截并显示友好提示

## 📁 项目结构

```
oj-competition-side-client/
├── main.js                   # 主进程入口文件
├── package.json              # 项目配置和依赖
├── README.md                 # 项目说明文档
├── PROJECT_OVERVIEW.md       # 项目详细概览
├── public/                   # 静态资源目录
│   ├── favicon.ico          # Windows 图标
│   ├── favicon.icns         # macOS 图标
│   ├── favicon.png          # Linux 图标
│   └── svg/                 # SVG 图标集合
│       ├── back.svg         # 后退图标
│       ├── forward.svg      # 前进图标
│       ├── refresh.svg      # 刷新图标
│       ├── home.svg         # 主页图标
│       └── info.svg         # 信息图标
└── utils/                   # 工具模块目录
    ├── toolbarManager.js    # 工具栏管理器
    ├── contentViewManager.js # 内容视图管理器
    ├── shortcutManager.js   # 快捷键管理器
    ├── windowHelper.js      # 窗口工具助手
    ├── urlHelper.js         # URL 处理工具
    ├── dialogHelper.js      # 对话框工具
    ├── domainHelper.js      # 域名控制工具
    └── platformHelper.js    # 平台兼容工具
```

## 🏗️ 技术架构

### 核心模块

#### 1. **重定向拦截器** - `applyRedirectInterceptor`
- 智能监听页面重定向行为
- 自动拦截非法重定向目标
- 实时获取重定向前URL并回退到安全域名
- 动态更新窗口初始URL避免循环重定向

#### 2. **工具栏管理器** - `ToolbarManager`
- 创建独立的 BrowserView 工具栏层
- 处理本地 SVG 图标渲染和主题适配
- 管理工具栏按钮事件和状态
- 实现工具栏动画和视觉反馈

#### 3. **内容视图管理器** - `ContentViewManager`
- 创建和管理网页内容视图
- 实现导航拦截和安全控制
- 处理域名白名单/黑名单逻辑
- 管理页面加载状态和错误处理

#### 4. **快捷键管理器** - `ShortcutManager`
- 注册跨平台全局快捷键
- 处理键盘事件和工具栏动作映射
- 智能焦点检测，避免输入框冲突
- 支持动态快捷键禁用/启用

#### 5. **窗口工具助手** - `windowHelper`
- 创建和管理应用窗口
- 处理新窗口的导航栏创建
- 管理窗口布局和大小调整
- 实现窗口间通信和状态同步

#### 6. **对话框工具** - `dialogHelper`
- 显示域名拦截的友好提示对话框
- 创建系统信息弹窗（包含版本信息和相关链接）
- 处理外部链接的安全打开
- 支持 Windows 自定义弹窗和原生弹窗

#### 7. **域名控制工具** - `domainHelper`
- 实现域名白名单/黑名单检查
- 统一拦截并弹窗提示逻辑
- 支持主窗口和新窗口的不同拦截策略

#### 8. **URL 处理工具** - `urlHelper`
- 提供 URL 解析和域名提取功能
- 支持安全的 URL 处理和验证

#### 9. **平台兼容工具** - `platformHelper`
- 处理跨平台的文件路径问题
- 管理不同操作系统的特定配置
- 提供统一的平台检测接口

### 🎯 架构特点

- **模块化设计** - 功能完全分离，代码结构清晰，易于维护和扩展
- **BrowserView 架构** - 工具栏与网页内容完全独立，避免页面刷新影响
- **安全优先设计** - 多层安全控制，从重定向拦截到开发者工具禁用
- **智能状态管理** - 实时更新按钮状态、URL状态和快捷键状态
- **跨平台兼容** - 完善的平台检测和适配，确保各系统一致体验
- **异步处理优化** - 避免在事件处理期间同步加载，防止死循环和白屏

## ⚙️ 配置说明

在 `main.js` 中修改 `APP_CONFIG` 对象来调整应用行为：

```javascript
const APP_CONFIG = {
  // 主页面地址
  HOME_URL: 'https://op.sdutacm.cn/',
  
  // 主窗口允许访问的根域名
  MAIN_DOMAIN: 'op.sdutacm.cn',
  
  // 新窗口白名单域名
  POPUP_WHITELIST: new Set([
    'rl.algoux.cn',      // 算法竞赛平台
    'rl.algoux.org',     // 算法竞赛平台备用
    'rank.ac',           // 排行榜系统
    'acm.sdut.edu.cn'    // SDUT ACM 官网
  ]),
  
  // 显式禁止的域名
  BLOCKED_DOMAINS: new Set([
    'oj.sdutacm.cn'      // 旧版 OJ 系统
  ])
};
```

## 🌍 跨平台兼容性

### Windows 特有优化
- ✅ 使用 `favicon.ico` 格式图标，确保最佳显示效果
- ✅ 处理 GPU 进程相关警告，提供流畅体验
- ✅ 支持 NSIS 安装程序和便携版
- ✅ 自定义 HTML 弹窗，支持彩色 emoji 显示
- ✅ 同时支持 x64 和 arm64 架构

### macOS 特有优化
- ✅ 支持 macOS 特有的快捷键组合（Cmd 键）
- ✅ 原生应用菜单栏，完美集成系统
- ✅ 使用 `favicon.icns` 确保 Dock 图标显示正确
- ✅ 支持 DMG 和 ZIP 两种分发格式
- ✅ Universal Binary，同时支持 Intel 和 Apple Silicon

### Linux 特有优化
- ✅ 使用 `favicon.png` 格式，支持透明度和高清显示
- ✅ 适配各种 Linux 发行版的窗口管理器
- ✅ 支持 AppImage 和 DEB 包格式
- ✅ 完善的字体渲染和界面显示效果
- ✅ ARM64 架构支持，适配最新硬件

## 🔧 开发特性

### 智能重定向拦截
- **实时监控**: 使用 `did-start-navigation` 和 `did-navigate` 事件记录页面URL
- **精确拦截**: 在 `will-redirect` 事件中实时获取当前URL并判断重定向合法性
- **智能回退**: 回退到重定向前URL的顶级域名，而非系统主域名
- **循环避免**: 动态更新窗口初始URL，防止"返回主页"时再次触发重定向

### 弹窗拦截系统  
- **白名单管理**: 只有白名单域名才能弹出新窗口
- **完整工具栏**: 新窗口自动创建完整的导航系统
- **防抖机制**: 防止同一URL在短时间内重复弹窗
- **友好提示**: 随机化的可爱拦截提示信息

### 快捷键优化
- **焦点检测**: 自动检测输入框焦点，避免快捷键冲突
- **跨平台适配**: Windows/Linux 使用 Alt 键，macOS 使用 Cmd 键
- **状态同步**: 快捷键状态与工具栏按钮状态实时同步
- **原生集成**: macOS 下集成原生菜单栏，支持系统快捷键

## 🏷️ 关键词标签

`ACM竞赛` `在线评测` `SDUT` `算法竞赛` `编程竞赛` `OJ客户端` `Electron应用` `比赛环境` `ICPC` `程序设计竞赛` `山东理工大学` `竞赛系统` `安全浏览器` `跨平台应用` `重定向拦截` `弹窗管理` `域名控制`

## 📝 版本信息

- **当前版本**: v1.0.0
- **Electron**: v27.0.0
- **Node.js 要求**: >=16.0.0
- **构建工具**: electron-builder v26.0.12

## 📧 联系方式

- **项目主页**: [GitHub Repository](https://github.com/ATRIOR-LCL/oj-competition-side-client)
- **SDUT OJ**: [https://op.sdutacm.cn/](https://op.sdutacm.cn/)
- **开发者**: ATRIOR-LCL (sdutwujinhao@gmail.com)
- **问题反馈**: 请在 GitHub Issues 中提交问题和建议

---

**© 2008-2025 SDUTACM. All Rights Reserved.**
