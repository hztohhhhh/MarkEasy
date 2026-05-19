# MarkEasy

MarkEasy 是一个可直接在浏览器中运行的 Markdown 查看与编辑工具。它以单个 HTML 页面为核心，不需要后端服务、Node.js 或构建流程，适合本地文档预览、轻量编辑、中文技术文档排版，以及包含公式、Mermaid 图表、图片和表格的 Markdown 文档整理。

核心入口文件是 [MarkEasy.html](MarkEasy.html)。保留 `MarkEasy.html` 和 `vendor/` 目录后即可运行；其中 `vendor/` 用于支持中文 PDF 导出。

## 功能特性

- 打开或拖拽加载 `.md`、`.markdown`、`.mdown`、`.mkd`、`.txt` 等文本文件。
- 支持「预览编辑」和「源码编辑」两种模式。
- 预览区可直接编辑内容，并通过 Turndown 同步回 Markdown 源码。
- 自动生成一级至四级标题大纲，支持跳转、折叠和拖拽调整大纲宽度。
- 支持多种标题编号方式：按章节、按大写、自动序号、不编号。
- 支持 GitHub Flavored Markdown，包括表格、任务列表、围栏代码块等。
- 使用 MathJax 渲染 LaTeX 行内公式和块级公式。
- 使用 Mermaid 渲染流程图、时序图、状态图、类图、甘特图、饼图、ER 图等图表。
- 使用 highlight.js 进行代码高亮，并提供代码块复制按钮。
- 支持插入远程图片或本地图片，支持图片说明、宽度和对齐方式设置。
- 支持插入 HTML 表格，并在预览区直接编辑、选中、合并、拆分、增删行列。
- 支持导出 HTML、A4 PDF 和 Markdown 文件。
- 支持浅色/深色主题，并将主题、大纲和编号设置保存到浏览器本地。

## 项目结构

```text
.
├── MarkEasy.html
├── README.md
├── markdown-test-case.md
└── vendor/
    ├── pdfmake.min.js
    └── pdfmake-chinese-vfs.js
```

文件说明：

| 文件 | 说明 |
| --- | --- |
| `MarkEasy.html` | 主应用文件，包含页面结构、样式和核心交互逻辑 |
| `markdown-test-case.md` | 功能测试用 Markdown 示例文档 |
| `vendor/pdfmake.min.js` | PDF 导出依赖，当前文件头标注为 pdfmake v0.2.20 |
| `vendor/pdfmake-chinese-vfs.js` | PDF 中文字体虚拟文件系统，用于中文内容导出 |

## 快速开始

### 本地运行

1. 下载或克隆本项目。
2. 确保 `MarkEasy.html` 和 `vendor/` 位于同一级目录。
3. 使用 Chrome、Edge 或 Firefox 等现代浏览器打开 `MarkEasy.html`。
4. 点击顶部「打开」按钮选择 Markdown 文件，或将 Markdown 文件拖拽到页面中。
5. 在「预览」或「源码」模式下编辑文档。
6. 根据需要点击 `HTML`、`PDF` 或 `MD` 按钮导出文件。

### 使用测试文档

项目提供了 [markdown-test-case.md](markdown-test-case.md)，可用于快速检查以下能力：

- 标题大纲与标题编号
- 预览区直接编辑
- 行内公式与块级公式
- Mermaid 图表渲染
- 图片显示与对齐
- HTML 表格编辑
- 代码高亮
- HTML、PDF、Markdown 导出

## GitHub Pages 发布

本项目是静态 HTML 项目，可以直接部署到 GitHub Pages。

仓库名建议使用 `MarkEasy`。当前主页面文件名是 `MarkEasy.html`，因此发布到 GitHub Pages 后可通过下面的地址访问：

```text
https://<你的 GitHub 用户名>.github.io/MarkEasy/MarkEasy.html
```

如果希望访问 `https://<你的 GitHub 用户名>.github.io/MarkEasy/` 时直接打开应用，可以额外添加一个 `index.html`，或将 `MarkEasy.html` 改名为 `index.html`。改名时需要确认 README 和后续说明中的入口文件名同步更新。

## 外部依赖

`MarkEasy.html` 通过 CDN 加载以下前端库：

| 依赖 | 当前引用 | 用途 |
| --- | --- | --- |
| markdown-it | `14.1.0` | Markdown 解析与渲染 |
| highlight.js | `11.9.0` | 代码语法高亮 |
| Mermaid | `10.9.1` | 流程图与图表渲染 |
| MathJax | `3` | LaTeX 数学公式渲染 |
| Turndown | `7.2.0` | 将预览区 HTML 同步回 Markdown |
| turndown-plugin-gfm | `1.0.2` | 支持 GFM 表格、任务列表等转换 |
| Lucide | `0.468.0` | 界面图标 |

PDF 导出相关文件放在本地 `vendor/` 目录中。发布到 GitHub 时需要一起提交 `vendor/pdfmake.min.js` 和 `vendor/pdfmake-chinese-vfs.js`，否则 PDF 导出和中文字体支持会失败。

如果需要完全离线使用，需要将 CDN 依赖也下载到本地，并修改 `MarkEasy.html` 中对应的 `<script src="...">` 路径。

## 数据与隐私

MarkEasy 在浏览器本地运行。用户打开或编辑的 Markdown 内容不会主动上传到服务器。

需要注意：

- 默认版本会从 CDN 加载部分前端依赖，浏览器会向对应 CDN 发起请求。
- 如果文档中使用远程图片地址，浏览器会请求对应图片资源。
- 本地主题、大纲和编号偏好会保存到浏览器 `localStorage`。

## 浏览器要求

建议使用较新的桌面浏览器：

- Google Chrome
- Microsoft Edge
- Firefox

项目使用了文件读取、拖拽、Blob 下载、Canvas、SVG、`contenteditable`、`localStorage` 等浏览器能力，过旧浏览器可能无法完整支持全部功能。

## 开发说明

本项目目前不依赖 npm、打包器或构建命令，主要逻辑集中在 `MarkEasy.html` 中：

- `<style>`：界面布局、Markdown 内容样式、响应式布局和打印样式。
- HTML 结构：顶部工具栏、大纲面板、编辑区、预览区、状态栏、右键菜单和弹窗。
- `<script>`：文件读取、Markdown 渲染、预览同步、右键编辑、公式与图表渲染、导出和本地状态持久化。

后续如果继续扩展功能，建议优先按以下方向拆分或维护：

- Markdown、MathJax、Mermaid、代码高亮等渲染逻辑
- 预览区编辑、右键菜单、HTML 转 Markdown 等编辑逻辑
- HTML、PDF、Markdown 等导出逻辑
- 主题、大纲、布局、状态栏等 UI 状态逻辑

## 常见问题

### 预览编辑无法同步回源码怎么办？

预览编辑依赖 Turndown 和 `turndown-plugin-gfm`。如果网络无法访问 CDN，相关依赖加载失败，预览区编辑可能无法正确回写到 Markdown 源码。可以检查浏览器控制台，或改为本地引入依赖。

### PDF 导出失败怎么办？

请确认 `vendor/pdfmake.min.js` 和 `vendor/pdfmake-chinese-vfs.js` 存在，并且与 `MarkEasy.html` 的相对路径没有改变。部分外链图片可能因为跨域限制无法嵌入 PDF，页面会尽量使用占位提示处理。

### Mermaid 或公式没有渲染怎么办？

Mermaid 和 MathJax 默认通过 CDN 加载。网络不可用、CDN 被拦截或脚本加载失败时，图表和公式渲染会受到影响。离线环境建议将相关依赖下载到本地。

## 发布前检查

- 确认仓库名为 `MarkEasy`。
- 确认 `MarkEasy.html`、`markdown-test-case.md`、`README.md` 和 `vendor/` 都已提交。
- 确认 README 中的 GitHub Pages 访问地址已经替换为你的 GitHub 用户名。
- 确认是否需要添加 `LICENSE` 文件。公开仓库不等于自动授予开源许可证；如希望他人可以使用、修改或分发，请选择合适的许可证。

## 许可证

当前项目尚未包含 `LICENSE` 文件。正式公开发布前，建议根据你的授权意图补充许可证，例如 MIT、Apache-2.0、GPL-3.0 或其他许可证。
