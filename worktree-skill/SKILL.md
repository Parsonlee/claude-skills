---
name: Git Worktree Creator
description: Creates a git worktree in parent directory with format {project}_{branch} when user needs parallel development or separate working environment
---

# Git Worktree Creator

自动基于主分支（master/main）创建 git worktree，目录位于当前项目根目录的上级，命名格式为：`{项目名}_{分支名}`

## 功能特性

- ✅ 自动检测主分支（main 或 master）
- ✅ 在父目录创建 worktree
- ✅ 智能命名：`{项目名}_{分支名}`
- ✅ 自动创建新分支或检出已存在的分支
- ✅ 提供清晰的操作提示和后续步骤

## 使用方法

### 基本用法

创建一个新的 worktree 和分支：

```bash
请帮我创建一个 feature-login 的 worktree
```

或者更具体地：

```bash
为 feature-user-profile 分支创建一个新的 worktree
```

### 指定基础分支

如果想从特定分支创建：

```bash
从 develop 分支创建一个 feature-api-v2 的 worktree
```

## 工作流程

1. **检测环境**
   - 验证是否在 git 仓库中
   - 获取项目根目录和名称
   - 自动检测主分支（main 或 master）

2. **创建 Worktree**
   - 生成 worktree 路径：`{父目录}/{项目名}_{分支名}`
   - 创建新分支或检出已存在的分支
   - 设置工作目录

3. **提供指引**
   - 显示 worktree 位置
   - 提供切换命令
   - 说明如何删除 worktree

## 实现说明

此 skill 使用 shell 脚本实现，提供：

- 完整的错误处理
- 彩色输出便于阅读
- 自动检测 main/master 分支
- 验证分支名称格式
- 检查目录冲突

## 示例场景

### 场景 1：开发新功能

**用户请求：** "帮我创建一个 feature-user-profile 的 worktree"

**结果：**
- 项目名：`my-app`
- 创建分支：`feature-user-profile`
- Worktree 路径：`../my-app_feature-user-profile`

### 场景 2：修复 Bug

**用户请求：** "我需要一个 bugfix-login-error 的独立工作区"

**结果：**
- 项目名：`my-app`
- 创建分支：`bugfix-login-error`
- Worktree 路径：`../my-app_bugfix-login-error`

### 场景 3：从特定分支创建

**用户请求：** "从 develop 分支创建 feature-api-v2 worktree"

**结果：**
- 从 `develop` 分支创建
- 新分支：`feature-api-v2`
- Worktree 路径：`../my-app_feature-api-v2`

## 后续操作

### 切换到 Worktree

```bash
cd ../my-app_feature-name
```

### 查看所有 Worktrees

```bash
git worktree list
```

### 删除 Worktree

完成工作后：

```bash
git worktree remove ../my-app_feature-name
```

## 优势

1. **并行开发**：在不同 worktree 中同时处理多个功能
2. **隔离环境**：每个 worktree 都有独立的工作区
3. **快速切换**：无需 stash 或 commit，直接切换目录
4. **规范命名**：统一的命名格式，易于管理

## 注意事项

- 分支名只能包含字母、数字、连字符、下划线和斜杠
- 确保在 git 仓库中执行
- 父目录必须有写入权限
- Worktree 目录不能已存在

## 技术实现

参见 `worktree.sh` 脚本文件，使用 Bash 实现，包括：
- Git 命令封装
- 自动分支检测
- 完整错误处理
- 用户友好的输出
