# Font-Spider 字体压缩项目

一个使用 Font-Spider（字蛛）进行中文字体压缩的示例项目。通过智能分析网页中使用的文字，自动提取并生成最小化的字体文件，大幅减少字体文件体积。

## 📦 项目简介

中文字体文件通常非常大（几 MB 到几十 MB），会严重影响网页加载速度。Font-Spider 可以智能分析 HTML 文件中使用的文字，从原字体文件中提取这些文字对应的字形，生成压缩后的字体文件，体积通常可以减小到几十 KB。

## ✨ 功能特点

- 🎯 **智能分析**：自动分析 HTML 文件中使用的所有文字
- 📉 **极致压缩**：从原字体中提取使用的字符，大幅减小文件体积
- 🚀 **快速加载**：压缩后的字体文件可大幅提升网页加载速度
- 💯 **保持质量**：压缩后字体质量无损，完美还原字形
- 🔄 **自动备份**：自动备份原字体文件，安全可靠

## 📋 环境要求

- Node.js 环境（推荐 v12 及以上版本）
- npm 或 yarn 包管理器

## 🔧 安装步骤

### 1. 全局安装 Font-Spider

```bash
npm install font-spider -g
```

或使用 yarn：

```bash
yarn global add font-spider
```

### 2. 验证安装

```bash
font-spider --version
```

## 📝 使用说明

### 基本用法

#### 1. 准备 HTML 文件

在 HTML 文件中使用 `@font-face` 声明自定义字体：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <style>
        @font-face {
            font-family: 'YOUSHEBIAOTIHEI';
            src: url('./YOUSHEBIAOTIHEI-2.TTF') format('truetype');
            font-weight: normal;
            font-style: normal;
        }

        .custom-font {
            font-family: 'YOUSHEBIAOTIHEI', sans-serif;
            font-size: 36px;
        }
    </style>
</head>
<body>
    <p class="custom-font">需要使用自定义字体的文字内容</p>
</body>
</html>
```

**⚠️ 注意事项：**
- 字体路径必须使用**相对路径**
- 不支持 CSS 文件中的 `@font-face`，必须写在 HTML 的 `<style>` 标签内
- 确保字体文件与 HTML 文件在同一目录或使用正确的相对路径

#### 2. 运行压缩命令

```bash
font-spider index.html
```

或压缩多个 HTML 文件：

```bash
font-spider index.html page2.html page3.html
```

使用通配符：

```bash
font-spider *.html
```

#### 3. 查看结果

压缩完成后，Font-Spider 会：
- ✅ 自动备份原字体文件（添加 `.font-spider` 后缀）
- ✅ 生成压缩后的字体文件（替换原文件）
- ✅ 在 `.font-spider` 目录中保存备份和压缩信息

## 📂 项目结构

```
font-spider/
├── index.html                    # HTML 示例文件
├── YOUSHEBIAOTIHEI-2.TTF        # 字体文件（压缩后）
├── .font-spider/                 # Font-Spider 生成的目录
│   └── YOUSHEBIAOTIHEI-2.font-spider.ttf  # 原字体备份
└── README.md                     # 项目说明文档
```

## 🎯 本项目示例

本项目包含：
- `index.html`：使用优设标题黑字体的示例页面
- `YOUSHEBIAOTIHEI-2.TTF`：优设标题黑字体文件

### 运行示例

```bash
# 1. 进入项目目录
cd font-spider

# 2. 运行压缩（如果字体已压缩，可先恢复原文件）
font-spider index.html

# 3. 在浏览器中打开 index.html 查看效果
```

## 💡 高级用法

### 恢复原字体

如果需要恢复原字体文件：

```bash
# 从 .font-spider 目录中复制备份文件
cp .font-spider/YOUSHEBIAOTIHEI-2.font-spider.ttf YOUSHEBIAOTIHEI-2.TTF
```

### 添加新文字

如果需要在页面中添加新的文字：

1. 先恢复原字体文件
2. 修改 HTML 文件，添加新文字
3. 重新运行 `font-spider index.html` 进行压缩

### 批量处理

处理整个网站的所有页面：

```bash
font-spider ./dist/**/*.html
```

## 🚨 常见问题

### 1. 字体无法加载？

**原因**：字体路径不正确或使用了绝对路径

**解决**：确保在 `@font-face` 中使用相对路径，如 `./font.ttf` 或 `../fonts/font.ttf`

### 2. 压缩后某些字显示异常？

**原因**：这些字在压缩时的 HTML 文件中没有出现

**解决**：确保 HTML 文件中包含所有可能使用的文字，或者在隐藏元素中预先声明

### 3. CSS 文件中的 @font-face 不生效？

**原因**：Font-Spider 只能分析 HTML 文件中 `<style>` 标签内的 `@font-face`

**解决**：将 `@font-face` 声明移到 HTML 的 `<style>` 标签中

### 4. 字体文件体积没有明显减小？

**原因**：页面中使用的字符过多

**解决**：检查是否有不必要的文字内容，或考虑分页处理

## 📱 微信小程序中使用自定义字体

### 使用 Font-Spider 压缩字体（推荐）

微信小程序对字体文件大小有严格限制，使用 Font-Spider 压缩字体是最优解决方案。

#### 实现步骤：

##### 1. 准备 HTML 文件并压缩字体

首先创建一个包含小程序中所有需要显示文字的 HTML 文件：

```html
<!DOCTYPE html>
<html lang="zh-CN">
<head>
    <meta charset="UTF-8">
    <style>
        @font-face {
            font-family: 'CustomFont';
            src: url('./YOUSHEBIAOTIHEI-2.TTF') format('truetype');
            font-weight: normal;
            font-style: normal;
        }
        .text {
            font-family: 'CustomFont';
        }
    </style>
</head>
<body>
    <!-- 在这里列出小程序中所有需要使用自定义字体的文字 -->
    <div class="text">首页欢迎页面标题所有文字内容...</div>
</body>
</html>
```

运行压缩命令：

```bash
font-spider index.html
```

##### 2. 将压缩后的字体转换为 Base64

压缩完成后，将字体文件转换为 Base64 编码。可以使用在线工具或命令行：

**Node.js 转换方法：**

```javascript
// convert-font.js
const fs = require('fs');

const fontPath = './YOUSHEBIAOTIHEI-2.TTF';
const fontBuffer = fs.readFileSync(fontPath);
const base64Font = fontBuffer.toString('base64');
const base64Str = `data:font/truetype;charset=utf-8;base64,${base64Font}`;

fs.writeFileSync('font-base64.txt', base64Str);
console.log('字体转换完成！');
console.log('文件大小:', (base64Font.length / 1024).toFixed(2), 'KB');
```

运行转换：

```bash
node convert-font.js
```

##### 3. 在小程序中使用

在小程序的 `app.js` 或页面 JS 文件中加载字体：

```javascript
// app.js
App({
  onLaunch() {
    // 加载自定义字体
    wx.loadFontFace({
      family: 'CustomFont',
      source: 'data:font/truetype;charset=utf-8;base64,AAEAAAALAIAAAwAwT1MvMg8SBz...', // 这里填入 base64 编码
      success: function() {
        console.log('字体加载成功');
      },
      fail: function(err) {
        console.log('字体加载失败', err);
      }
    });
  }
})
```


## 📚 参考资料

- [掘金教程文章](https://juejin.cn/post/6904541605265899527)
- [微信小程序自定义字体方案](https://juejin.cn/post/6844903838965563405)
- [字体转换工具](https://transfonter.org/)

