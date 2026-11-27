# 托育考核扫码考试系统

考生扫码 → 前端从 3000 题题库现场随机抽题（单选70 + 多选20 + 判断10，满分100，合格线80，限时60分钟），交卷即时判分并显示解析。

## 最省事的部署：GitHub Actions 自动开 Pages
1. 在 GitHub 新建 **Public** 仓库（例如 `tuoyu-exam`）
2. 把本文件夹里的**全部文件**（含隐藏的 `.nojekyll` 和 `.github`）拖进仓库根目录上传
3. 等 1～2 分钟，仓库 **Settings → Pages** 会出现：
   `https://你的用户名.github.io/tuoyu-exam/`
   （Source 显示 `GitHub Actions` 即正确，不用手动选分支）
4. 打开链接确认能答题 → 点页面底部「我是组织者」→ 生成并下载二维码 → 打印/投屏

## 也可以手动开 Pages
Settings → Pages → Source 选 `Deploy from a branch` → Branch 选 `main`、Folder 选 `/ (root)` → Save。

## 文件说明
| 文件 | 作用 |
|---|---|
| index.html | 考试页面（配置在文件开头 CFG 处） |
| questions.json | 3000 题题库（答案不在前端题干里，判分在交卷时进行） |
| qrcode.min.js | 二维码生成（本地文件，无任何外部 CDN 依赖） |
| .nojekyll | 防止 GitHub 跳过 json 文件 |

## 常用改法（改 index.html 开头的 CFG）
- 分场防对答案：`pool:'A'` / `'B'` / `'C'` / `'D'`，四组各 750 题互不重叠；每个场次改一次、重新上传即可（链接不变，码不用重做）
- 改合格线：`passScore`；改时长：`durationMin`；改题量/分值：`counts` / `score`（总分尽量保持 100）
- 题库位于 `questions.json` 中，可自行增补（字段：g 分组、c 分类、s 题干、o 选项、a 正确项下标、e 解析）
