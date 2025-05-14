以下教程基于如下平台与资料：

- [Learning Git Branch](https://learngitbranching.js.org/)：一个交互式的学习github命令行操作的网站，强烈推荐。
- [Git doc](https://git-scm.com/doc): Git 官方文档
- [JetBrainsIDEs Git Integration Documentation](https://www.jetbrains.com/zh-cn/help/idea/2025.1/version-control-integration.html): JetBrains 家 IDE 内部集成Git工具的官方文档。
- [秒懂Git之配置(配置git默认编辑器为vscode或者notepad++)](https://blog.csdn.net/ShuSheng0007/article/details/115449596)
- [Git Commit 之道：规范化 Commit Message 写作指南](https://blog.csdn.net/hzf0701/article/details/134367234)
- [git合作流程（collaborator模式和contributor模式）](https://blog.csdn.net/qq_41230365/article/details/86766005)

## 1.学习使用命令行进行项目本地仓库的版本管理

### 1.1 什么是命令行

### 1.2 什么是命令行中的命令

### 1.3 认识 命令行 命令的基本结构

### 1.4 学会使用 git 命令行工具

### 1.5 

## 学习在 Android Studio 使用git 进行项目管理

### 学习本地仓库进行版本管理

- **在 JetBrains IDE 中初始化 Git 仓库**
- **理解 IDE 中的暂存区 (Staging Area / Changelists)**
- **提交更改 (Commit) 与查看历史 (Log)**
  - 如何使用 IDE 的提交界面
  - 编写规范的提交信息
  - 通过 IDE 查看提交历史、分支图
- **分支管理 (Branching)**
  - 在 IDE 中创建、切换、合并和删除分支
- **标签管理 (Tagging)**
  - 在 IDE 中创建和推送标签

### 学习使用远程仓库进行协作并处理冲突 (JetBrains IDE 实战)

- **连接到远程仓库**
  - 在 IDE 中克隆 (Clone) 远程仓库
  - 在 IDE 中添加远程仓库 (Remotes)
- **基本的远程操作**
  - **推送 (Push)**：将本地提交推送到远程仓库
    - 使用 IDE 的 Push 对话框
  - **拉取 (Pull)**：从远程仓库获取最新更改并合并
    - Fetch 与 Pull 的区别
    - 在 IDE 中执行 Pull 操作 (Merge vs Rebase)
  - **获取 (Fetch)**：从远程仓库获取最新更改但不合并
- **协作工作流 (以 Feature Branch Workflow 为例)**
  - **创建和推送特性分支**：在 IDE 中为新功能或修复创建分支并推送到远程。
  - **团队成员间的代码同步**：定期 Pull 主分支或开发分支的更新。
  - **发起合并请求 (Pull Request / Merge Request)**：
    - 虽然 PR/MR 通常在代码托管平台（如 GitHub, GitLab）上创建，但可以说明如何在 IDE 中准备好分支以供审查。
    - 如何在 IDE 中检出 (Checkout) 他人的 PR/MR 分支进行审查和测试。
- **处理合并冲突 (Conflict Resolution)**
  - 冲突是如何产生的
  - **使用 JetBrains IDE 的三方合并工具**：详细步骤说明如何识别冲突文件，并使用 IDE 内置的强大合并工具解决冲突。
  - 提交解决冲突后的代码
- **其他有用的协作功能**
  - **储藏 (Stash)**：在 IDE 中临时保存未完成的更改。
  - **拣选 (Cherry-pick)**：在 IDE 中选择性地将某些提交应用到当前分支。
  - **变基 (Rebase)**：在 IDE 中使用 Rebase 功能保持提交历史的整洁（特别是与远程主分支同步时）。

### 常见协作问题与 JetBrains IDE 解决方案

- 例如：推送被拒绝 (Push Rejected) 如何处理等。

## 学习在vscode 中使用自带源代码管理界面进行项目管理
