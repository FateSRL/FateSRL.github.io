# 葛广一 · Hugo 个人主页

以项目和学习记录为主的中文个人博客。无主题子模块，无 Node 依赖，使用 Hugo 0.168.0 构建。

## 页面

- 首页：简短介绍、最近更新与学习入口，使用统一的文章列表布局。
- 项目：统一列表展示；论文调研助手排第一，其次是 MIT 6.5840 分布式系统实验、2D 动作游戏。
- 学习：课程学习和算法训练，可筛选。
- 关于：教育背景、课程成绩、竞赛经历、研究兴趣和联系方式。
- 简历：在线查看，浏览器“打印 / 保存 PDF”。

项目介绍沿用所提供的简历。6.5840 不提供源码链接；hello-agents-study 为待补充的课程条目，没有仓库链接；Codeforces 仅提供已确认的个人主页入口。

## 本地预览

安装 Hugo 0.168.0（普通版即可），在本目录运行：

```powershell
hugo server --bind 127.0.0.1
```

访问终端显示的本地地址。生成生产网站：

```powershell
hugo build --gc --minify
```

## 发布至 GitHub Pages

1. 使用主页仓库：https://github.com/FateSRL/FateSRL.github.io 。
2. 将本目录内的源文件提交到仓库的 `main` 分支，包含 `.github/workflows/hugo.yaml`。不提交 `public/`。
3. 仓库 Settings → Pages → Build and deployment → Source，选择 **GitHub Actions**。
4. 在 Actions 中运行 **Build and deploy Hugo site**，或向 main 提交一次修改。
5. 部署成功后访问 `https://fatesrl.github.io/`。

主页仓库：https://github.com/FateSRL/FateSRL.github.io

线上地址：https://fatesrl.github.io/

向 main 分支推送修改后，GitHub Actions 会自动构建并发布。部署状态可在仓库 Actions 中查看。

## 日常更新

| 要修改的内容 | 文件 |
| --- | --- |
| 学校、成绩、奖项、首页简介 | `data/profile.json` |
| 邮箱、GitHub、导航、站点地址 | `hugo.toml` |
| 项目介绍与状态 | `content/projects/*.md` |
| 课程与算法记录 | `content/learning/*.md` |
| 颜色、间距与响应式布局 | `assets/css/main.css` |

新增一条课程记录：

```powershell
hugo new content learning/my-course.md
```

新增一个项目：

```powershell
hugo new content projects/my-project.md
```

新条目默认为草稿。填好内容后，将 `draft = true` 改为 `false`；更新已有内容时同步修改 `lastmod`。首页自动显示 `show_update = true` 的最近五条记录，按 `lastmod` 排序。课程和算法占位条目目前设为 false，以免被当成学习进展。

课程记录使用 `category = '课程学习'`，算法记录使用 `category = '算法训练'`。课程上传仓库后，可在课程 Markdown 的 front matter 中增加：

```toml
repo = 'https://github.com/FateSRL/实际仓库名'
```

公开联系方式仅使用 `geguangyi@sjtu.edu.cn`。未加入简历之外的绩点、比赛年份、课程进度或项目指标。
