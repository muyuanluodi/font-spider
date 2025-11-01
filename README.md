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

## 📚 参考资料

- [Font-Spider GitHub 仓库](http://font-spider.org/)
- [掘金教程文章](https://juejin.cn/post/6904541605265899527)
- [中文 WebFont 优化方案](http://font-spider.org/)

## 📄 许可证

本项目仅供学习和参考使用。

## 🤝 贡献

欢迎提交 Issue 和 Pull Request！

---

**💻 Made with ❤️ by 字体优化爱好者**

