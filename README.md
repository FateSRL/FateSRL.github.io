# 葛广一的博客

线上地址：<https://fatesrl.github.io/>

源码仓库：<https://github.com/FateSRL/FateSRL.github.io>

网站直接使用 [Reimu](https://github.com/D-Sketon/hugo-theme-reimu) 官方 Hugo 主题，保留原主题的插画横幅、文章卡片、侧栏、阅读页面和深浅色切换。主题以 Git submodule 固定到一个提交，不修改上游主题文件。主题及所附资源的许可、署名保留在 `themes/reimu/` 中。

## 页面与内容

- 首页：项目记录，使用原主题文章列表。
- 项目：论文调研助手、MIT 6.5840 分布式系统实验、2D 动作游戏，按 `weight` 排序。
- 学习：hello-agents-study 文字占位、Codeforces 平台入口。
- 关于：教育背景、课程成绩、竞赛经历、研究兴趣和联系方式。
- 简历：原简历内容的在线 Markdown 页面。

6.5840 仅展示简历中的项目介绍，遵循课程要求不提供源码。课程尚未上传仓库，因此没有课程仓库链接。公开联系方式为 `geguangyi@sjtu.edu.cn`。

## 本地预览

需要 **Hugo Extended 0.168.0**。首次克隆时一并下载主题：

```powershell
git clone --recurse-submodules https://github.com/FateSRL/FateSRL.github.io.git
cd FateSRL.github.io
hugo server
```

如果已经克隆过仓库：

```powershell
git submodule update --init --recursive
```

生成生产网站：

```powershell
hugo build --gc --minify
```

GitHub Pages 已使用 GitHub Actions 自动构建，工作流会安装 Hugo Extended 并下载主题 submodule。向 `main` 推送内容后自动发布。

## 更新位置

| 内容 | 文件 |
| --- | --- |
| 站点标题、作者、邮箱、菜单和主题开关 | `hugo.toml` |
| 教育、成绩、竞赛与个人介绍 | `content/about.md` |
| 在线简历 | `content/resume.md` |
| 项目介绍 | `content/projects/*.md` |
| 课程与算法记录 | `content/learning/*.md` |
| 头像 | `static/avatar/fatesrl.png` |

横幅使用主题自带的 `images/banner.webp`，头像使用个人 GitHub 头像。需要更换图片时，将自己的图片放入 `static/`，再修改 `hugo.toml` 中的路径即可。

新增课程记录或项目：

```powershell
hugo new content learning/my-course.md
hugo new content projects/my-project.md
```

新条目默认为草稿，填写后将 `draft = true` 改为 `false`。使用 `categories = ['课程学习']` 或 `categories = ['算法训练']` 设置学习分类。两个现有占位条目用 `[build] list = 'local'` 只在学习栏目显示；填入正式记录后可移除该配置，让内容进入首页。

项目栏目按 `weight` 从小到大排列，论文调研助手为 1。首页使用原主题的时间倒序列表。标签 `CSharp` 对应 C#，用于避免 `#` 被浏览器当成 URL 片段。

网站使用 `layouts/section.html` 为“项目”“学习”栏目提供独立列表。列表卡片通过根目录的 `layouts/partials/post.html` 和 `assets/css/partials/post.scss` 覆盖为 Fuwari 风格的无图文字卡片，保留标题、日期、分类、标签、摘要、阅读信息和右侧箭头；深浅色均适配，上游主题文件保持原样。依赖库使用主题自带的本地文件；主题图标使用原配置的图标字体。鼠标烟花、特殊光标和加载遮罩已通过官方配置关闭。
