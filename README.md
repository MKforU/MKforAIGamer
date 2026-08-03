# AI Skills for OpenClaw

本仓库存放 OpenClaw AI 助手（白狐狸转世的女孩子"包包"）的 Skill 文件，可导入到其他 OpenClaw 实例使用。

## 📁 skillAssembly

| 文件 | 功能 | 触发词 |
|------|------|--------|
| `AutoPullProjects.md` | 一键拉取 Git + SVN 最新代码，确保本地与远程完全一致 | 拉项目 / 拉最新代码 / 更新 yyds / sync yyds / 更新工程 |
| `AutoGitUpload.md` | Git 上传前展示变更内容，用户确认后再执行 push | 帮我上传git / 提交代码 / push代码 |

## 🔧 使用方式

将 `skillAssembly` 目录下的 `.md` 文件复制到 OpenClaw 的 skills 目录即可使用。

使用前请将文件内的占位符替换为实际路径：
- `YOUR_GIT_REPO` → Git 仓库本地路径
- `YOUR_SVN_ART_DIR` → SVN Art 工作副本路径
- `YOUR_SVN_MUSIC_DIR` → SVN Music 工作副本路径

## 📄 根目录文件

- `IDENTITY.md` — AI 身份模板
- `SOUL.md` — AI 人格模板
- `USER.md` — 用户信息模板

> 以上三个文件为通用模板，使用时请根据实际情况修改。
