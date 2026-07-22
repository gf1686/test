# webtestinfo

基于 GitHub Pages 的静态页面展示站点，支持自动导航生成。

## 项目简介

这是一个轻量级的静态网站项目，主要用于快速展示和分享 HTML 页面。所有静态页面存放在 `page/` 目录下，首页会自动生成导航列表，无需手动维护链接。

## 快速开始

### 添加新页面

1. 将 HTML 文件放入 `page/` 目录
2. 提交并推送到 GitHub：

```bash
git add page/your-page.html
git commit -m "新增页面：your-page"
git push
```

3. 等待 GitHub Actions 部署完成（约 30 秒）
4. 刷新首页，导航自动出现新页面链接

### 本地预览

直接用浏览器打开 `index.html` 即可预览首页。页面导航依赖 `page/nav.json`，仓库中已包含一份本地副本。

## 目录结构

```
webtestinfo/
├── index.html              # 首页（含自动导航）
├── 404.html                # 404 错误页面
├── README.md               # 项目说明
├── page/                   # 静态页面目录
│   ├── nav.json            # 导航清单（CI 自动生成）
│   └── *.html              # 你的静态页面
└── .github/workflows/      # GitHub Actions 部署配置
    └── static.yml          # 自动部署 + 导航生成
```

## 自动导航原理

```
新增页面 → push → GitHub Actions 触发
                      │
                      ├─ 扫描 page/*.html
                      ├─ 生成 page/nav.json
                      └─ 部署到 GitHub Pages
                            │
                      index.html 读取
                      nav.json → 动态渲染导航
```

- **CI 端**：GitHub Actions 在部署前执行 Shell 脚本，扫描 `page/` 下所有 `.html` 文件，生成 `nav.json` 清单
- **前端**：`index.html` 通过 JavaScript 异步加载 `nav.json`，动态渲染导航卡片

## 技术栈

- 纯静态 HTML / CSS / JavaScript
- GitHub Pages 托管
- GitHub Actions 自动部署
