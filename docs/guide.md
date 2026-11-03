# 使用指南

本页记录从零开始把这份文档跑起来、改起来、发出去的过程。所有命令都在仓库根目录执行。

## 环境准备

| 依赖 | 建议版本 | 用途 |
| --- | --- | --- |
| Python | 3.10 及以上 | 运行 MkDocs |
| pip | 随 Python 安装 | 安装构建依赖 |
| Git | 任意近期版本 | 提交与推送 |
| 文本编辑器 | 任意 | 编辑 Markdown |

## 首次运行

```bash
# 1. 克隆仓库
git clone https://github.com/zhou043/my-docs.git my-docs
cd my-docs

# 2. 安装依赖
python -m pip install -r requirements.txt

# 3. 启动本地预览（默认 http://127.0.0.1:8000）
python -m mkdocs serve
```

预览服务会监听文件变化，保存 Markdown 后浏览器自动刷新。建议一直开着，边写边看。

## 日常写作流程

1. 在 `docs/` 下新建或修改 Markdown 文件；
2. 如果新增了页面，在 `mkdocs.yml` 的 `nav` 中登记，否则页面不会被导航引用；
3. 本地预览，检查排版、表格和站内链接；
4. 执行一次严格构建，确认没有告警；
5. 提交并推送到 `main`；
6. 在仓库的 Actions 页面确认流水线通过；
7. 打开线上地址，确认内容已更新。

第 4 步不要跳过。本地预览“看起来正常”和严格构建通过并不是一回事。

## 常用命令

| 命令 | 作用 | 何时使用 |
| --- | --- | --- |
| `python -m mkdocs serve` | 启动本地预览并热更新 | 写作过程中 |
| `python -m mkdocs build` | 生成 `site/` 目录 | 想检查构建产物时 |
| `python -m mkdocs build --strict` | 构建并把警告视为错误 | 每次提交前 |
| `git status` | 查看本次改动 | 提交前 |
| `git push origin main` | 推送并触发部署 | 发布时 |

```bash
# 提交前的完整检查
python -m mkdocs build --strict

# 构建通过后再推送
git add docs/ mkdocs.yml
git commit -m "docs: 更新使用指南"
git push origin main
```

## 写作约定

| 约定 | 说明 |
| --- | --- |
| 一页一个主题 | 避免单页过长，也便于别人直接链接到需要的部分 |
| 标题层级从 `#` 开始 | 每页只用一个一级标题 |
| 站内链接用相对路径 | 例如 `[使用指南](guide.md)` |
| 代码块标注语言 | 便于高亮，也便于日后检查 |
| 表格列数控制在 4 列以内 | 窄屏下更易阅读 |

## 常见问题

| 现象 | 可能原因 | 处理方式 |
| --- | --- | --- |
| 本地预览正常，Actions 失败 | 依赖未写入 `requirements.txt` | 补全依赖后重新推送 |
| 页面 404 | 文件未加入 `nav`，或链接路径写错 | 检查 `mkdocs.yml` 与相对路径 |
| 线上内容没更新 | 流水线未完成，或浏览器缓存 | 先看 Actions 状态，再强制刷新 |
| `--strict` 报链接告警 | 目标文件不存在，或大小写不一致 | 核对文件名，Linux 环境区分大小写 |
| Pages 页面 404 | 仓库 Pages 来源未设置为 Actions | 在 Settings → Pages 中调整 |

## 一点实践体会

最开始我习惯“写完一起检查”，结果一次提交里混着三四个问题，报错互相干扰。后来改成每写完一页就跑一次严格构建，问题定位从“猜”变成了“看”。

另外，文件名的大小写值得特别注意：Windows 本地不区分大小写，但 Actions 运行在 Linux 上，`Guide.md` 和 `guide.md` 会被当成两个不同的文件。我有一次就是这么拿到 404 的，之后统一使用小写文件名。

返回[首页](index.md) · 了解[项目背景](about.md) · 查看[API 参考](api.md)
