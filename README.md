# my-docs

使用 MkDocs Material 编写的个人技术文档站点，通过 GitHub Actions 自动构建并部署到 GitHub Pages。修改 `docs/` 中的 Markdown 并推送到 `main` 后，网站会自动更新。

- 网站地址：https://zhou043.github.io/my-docs/
- 个人实验报告：[报告与关键截图](report/README.md)
- 源码仓库：https://github.com/zhou043/my-docs
- 文档源码：`docs/`（首页、关于、使用指南、API 参考）
- 站点配置：`mkdocs.yml`

## 本地预览

```bash
python -m venv .venv
source .venv/Scripts/activate   # Windows Git Bash
python -m pip install -r requirements.txt
python -m mkdocs serve
```

打开终端提示的地址（通常为 http://127.0.0.1:8000/my-docs/ ） 预览。提交前可先执行严格构建检查：

```bash
python -m mkdocs build --strict
```
