# 国际化 (i18n) 使用指南

## 概述

本项目使用 `i18n-js` 库实现国际化支持，提供中文和英文两种语言。系统会自动检测操作系统语言并设置相应的界面语言。

## 目录结构

```
├── locales/                    # 语言文件目录
│   ├── zh-CN.json             # 中文翻译
│   └── en-US.json             # 英文翻译
├── utils/
│   ├── i18nManager.js         # 国际化管理器
│   └── macMenuManager.js      # Mac 菜单管理器 (支持国际化)
└── main.js                    # 应用入口 (集成国际化)
```

## 特性

### 🌍 多语言支持
- **中文 (zh-CN)**: 简体中文界面
- **英文 (en-US)**: 英文界面
- **自动检测**: 根据系统语言自动选择界面语言
- **动态切换**: 支持运行时切换语言

### 🍎 Mac 菜单国际化
- **完整菜单栏**: 应用菜单、文件、编辑、视图、窗口、帮助
- **动态更新**: 语言切换时菜单实时更新
- **快捷键支持**: 所有菜单项都支持标准 Mac 快捷键
- **语言选择**: 菜单栏中提供语言切换选项

### 🔧 开发者友好
- **参数插值**: 支持 `%{variable}` 格式的变量替换
- **回退机制**: 缺失翻译时自动回退到默认语言
- **错误处理**: 完善的错误处理和日志记录

## API 使用

### 基本用法

```javascript
const i18n = require('./utils/i18nManager');

// 获取翻译
const appName = i18n.t('app.name');
const menuFile = i18n.t('menu.file');

// 带参数的翻译
const version = i18n.t('app.version', { version: '1.0.0' });
const quit = i18n.t('menu.quit', { appName: 'My App' });
```

### 语言管理

```javascript
// 获取当前语言
const currentLang = i18n.getCurrentLanguage(); // 'zh-CN' 或 'en-US'

// 切换语言
i18n.setLanguage('en-US');

// 获取可用语言列表
const languages = i18n.getAvailableLanguages(); // ['zh-CN', 'en-US']

// 获取语言显示名称
const displayName = i18n.getLanguageDisplayName('zh-CN'); // '中文'
```

### 事件监听

```javascript
// 监听语言变更事件
i18n.on('languageChanged', (newLang, oldLang) => {
  console.log(`语言已从 ${oldLang} 切换到 ${newLang}`);
  // 更新界面...
});
```

## 翻译文件格式

### 中文 (locales/zh-CN.json)
```json
{
  "app": {
    "name": "SDUT OJ 竞赛客户端",
    "version": "版本 %{version}"
  },
  "menu": {
    "file": "文件",
    "edit": "编辑",
    "quit": "退出 %{appName}"
  }
}
```

### 英文 (locales/en-US.json)
```json
{
  "app": {
    "name": "SDUT OJ Competition Client",
    "version": "Version %{version}"
  },
  "menu": {
    "file": "File",
    "edit": "Edit",
    "quit": "Quit %{appName}"
  }
}
```

## Mac 菜单集成

### 自动初始化
在 `main.js` 中，Mac 菜单管理器会在 macOS 平台自动初始化：

```javascript
// macOS 特定设置
if (process.platform === 'darwin') {
  macMenuManager = new MacMenuManager(mainWindow);
}
```

### 语言切换菜单
菜单栏会自动添加语言切换选项：
- **应用菜单 > 语言 > 中文** - 切换到中文
- **应用菜单 > 语言 > English** - 切换到英文

### 快捷键支持
所有菜单项都支持标准 Mac 快捷键：
- `Cmd+Q` - 退出应用
- `Cmd+W` - 关闭窗口
- `Cmd+Z` - 撤销
- `Cmd+C` - 复制
- `Cmd+V` - 粘贴
- `Cmd+Left` - 后退
- `Cmd+Right` - 前进
- `Cmd+R` - 刷新
- `Cmd+Shift+H` - 主页

## 添加新语言

### 1. 创建语言文件
在 `locales/` 目录下创建新的语言文件，如 `ja-JP.json` (日语)：

```json
{
  "app": {
    "name": "SDUTオンラインジャッジ競技クライアント"
  },
  "menu": {
    "file": "ファイル",
    "edit": "編集"
  }
}
```

### 2. 更新配置
在 `utils/i18nManager.js` 中添加新语言：

```javascript
this.availableLanguages = ['zh-CN', 'en-US', 'ja-JP'];
```

### 3. 添加显示名称
更新 `getLanguageDisplayName` 方法：

```javascript
getLanguageDisplayName(language) {
  const displayNames = {
    'zh-CN': '中文',
    'en-US': 'English',
    'ja-JP': '日本語'
  };
  return displayNames[language] || language;
}
```

## 最佳实践

### 1. 翻译键命名
- 使用点分割的层级结构：`app.name`, `menu.file.open`
- 使用描述性的键名：`dialog.confirm.delete` 而不是 `dialog1`
- 保持一致的命名风格

### 2. 参数使用
- 使用 `%{variable}` 格式：`"Hello %{name}"`
- 参数名要有意义：`%{appName}` 而不是 `%{arg1}`
- 考虑不同语言的语法差异

### 3. 错误处理
- 始终提供回退文本
- 检查翻译键的存在性
- 处理参数缺失的情况

### 4. 性能优化
- 一次性加载所有语言文件
- 缓存翻译结果
- 避免频繁的语言切换

## 故障排除

### 常见问题

1. **翻译不显示**
   - 检查语言文件是否存在于 `locales/` 目录
   - 确认翻译键的拼写是否正确
   - 查看控制台是否有错误信息

2. **菜单未更新**
   - 确认在 macOS 平台运行
   - 检查 `MacMenuManager` 是否正确初始化
   - 验证语言变更事件是否触发

3. **参数插值失败**
   - 检查参数格式是否为 `%{paramName}`
   - 确认传递的参数对象包含所需的键
   - 验证参数值不为 `undefined`

### 调试技巧

```javascript
// 启用详细日志
console.log('当前语言:', i18n.getCurrentLanguage());
console.log('可用语言:', i18n.getAvailableLanguages());

// 检查翻译键存在性
if (!i18n.exists('some.key')) {
  console.warn('翻译键不存在:', 'some.key');
}

// 监听语言变更
i18n.on('languageChanged', (newLang, oldLang) => {
  console.log('语言变更:', oldLang, '->', newLang);
});
```

## 版本兼容性

- **Node.js**: >= 16.0.0
- **Electron**: >= 27.0.0
- **i18n-js**: ^4.5.1
