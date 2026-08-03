# AutoGitUpload：Git 上传（带确认流程）

## 功能
在上传前列出详细更改内容，等待用户检查并确认后才执行上传。

## 路径常量
- Git 仓库：`YOUR_GIT_REPO`

## 触发词
- "帮我上传git"
- "提交代码"
- "push代码"
（不固定，用户会明确告知意图）

## 执行步骤

### 1. 检查本地修改
```powershell
cd YOUR_GIT_REPO
git status --short
```

### 2. 列出详细更改内容
显示完整的 `git status` 输出，包括：
- 新增的文件（Untracked files）
- 修改的文件（Changes not staged for commit）
- 已暂存的文件（Changes to be committed）
- 删除的文件（Deleted）

### 3. 询问用户选择上传内容
使用 `render_ui` 的 `QuestionForm` 组件动态列出所有变更文件，让用户多选。

### 4. 等待用户输入"确认"
显示用户选择的文件列表，并提示：
> 请检查以上更改，确认无误后输入"确认"继续上传

等待用户输入"确认"（必须完全匹配这两个字）。

### 5. 询问 commit message
使用 `render_ui` 让用户选择：
- "使用默认信息" → 自动生成 message（包含时间戳）
- "自定义输入" → 弹出文本框让用户输入

### 6. 执行 Git 上传
```powershell
# 添加选择的文件
git add <用户选择的文件>

# 提交
git commit -m "<用户输入的commit message>"

# 推送
git push origin <当前分支名>
```

### 7. 显示上传结果
显示 push 的输出结果，包括：
- 上传成功的文件数
- 远程分支更新情况
- 任何错误或警告信息

## 注意事项
- 必须等待用户明确输入"确认"两个字才继续
- 若用户输入其他内容，提示"请输入'确认'以继续上传"并重新等待
- 若用户取消，则终止流程并提示"已取消上传"
- 上传前检查是否有未拉取的远程更新，如有则提示先执行拉取
