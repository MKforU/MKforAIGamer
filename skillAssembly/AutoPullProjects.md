# AutoPullProjects：yyds_client 一键拉项目

## 功能
同时拉取 Git 最新代码并更新两个 SVN 目录，确保本地与远程完全一致。

## 路径常量
> ⚠️ 请将以下占位符替换为实际路径后再使用
- Git 仓库：`YOUR_GIT_REPO`
- SVN Art：`YOUR_SVN_ART_DIR`
- SVN Music：`YOUR_SVN_MUSIC_DIR`

## 执行步骤

### 1. 检查当前分支
```powershell
cd YOUR_GIT_REPO
git branch --show-current
```

### 2. 询问是否切换分支
显示当前分支，询问用户是否需要切换。

使用 `render_ui` 的 `QuestionForm` 组件：
```json
{
  "id": "root",
  "component": "QuestionForm",
  "header": {"title": "切换分支？"},
  "list": [
    {
      "question": "当前分支是 [当前分支名]，需要切换吗？",
      "type": "single",
      "options": ["保持当前分支", "切换到 master", "切换到 dev"]
    }
  ]
}
```
- 若选择「保持当前分支」→ 继续后续步骤
- 若选择「切换到 master/dev」→ `git checkout master` / `git checkout dev`，然后继续

### 3. 检查本地修改并暂存
```powershell
git status --short
```
- 若有改动：`git stash push -u -m "本地修改暂存 $(Get-Date -Format 'yyyy-MM-dd HH:mm')"`
- 若无改动，跳过 stash

### 4. Git Pull
根据当前分支执行：
- master：`git pull origin master`
- dev：`git pull origin dev`
- 其他分支：`git pull origin <当前分支名>`

### 5. SVN 更新
```powershell
svn update "YOUR_SVN_ART_DIR"
svn update "YOUR_SVN_MUSIC_DIR"
```

### 6. 本地 Revert（确保与远程完全一致）

**Git 层：**
```powershell
git restore .
```

**SVN 层：**
```powershell
svn revert -R "YOUR_SVN_ART_DIR"
svn revert -R "YOUR_SVN_MUSIC_DIR"
```

### 7. 自动清理 stash
```powershell
git stash drop "stash@{0}"
```
静默删除，不询问用户。

## 触发词
- "拉项目"
- "拉最新代码"
- "更新 yyds"
- "sync yyds"
- "更新工程"
