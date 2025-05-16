以下教程基于如下平台与资料：

- [Learning Git Branch](https://learngitbranching.js.org/)：一个交互式的学习github命令行操作的网站，强烈推荐。
- [Git doc](https://git-scm.com/doc): Git 官方文档
- [JetBrainsIDEs Git Integration Documentation](https://www.jetbrains.com/zh-cn/help/idea/2025.1/version-control-integration.html): JetBrains 家 IDE 内部集成Git工具的官方文档。
- [秒懂Git之配置(配置git默认编辑器为vscode或者notepad++)](https://blog.csdn.net/ShuSheng0007/article/details/115449596)
- [Git Commit 之道：规范化 Commit Message 写作指南](https://blog.csdn.net/hzf0701/article/details/134367234)
- [git合作流程（collaborator模式和contributor模式）](https://blog.csdn.net/qq_41230365/article/details/86766005)

## 1 学习使用命令行进行项目本地仓库的版本管理

在本章节，你将学习版本控制的基础知识，并掌握如何使用命令行（也称为终端或控制台）来管理你的项目代码。命令行是与计算机交互的一种强大方式，尤其在软件开发中非常常用。

### 1.1 什么是命令行

命令行界面（Command Line Interface, CLI）是一个基于文本的用户界面，你可以通过输入命令来告诉计算机执行操作。与我们平时使用的图形用户界面（Graphical User Interface, GUI）不同，GUI依赖于鼠标点击图标和菜单，而CLI则依赖于键盘输入。

**为什么学习命令行？**
*   **效率高：** 对于许多任务，熟练使用命令行比图形界面更快。
*   **自动化：** 可以编写脚本来自动执行一系列命令。
*   **远程访问：** 在服务器上工作时，命令行通常是主要的交互方式。
*   **Git 的核心：** Git 最初是为命令行设计的，理解命令行操作有助于你更深入地理解 Git 的工作原理。

**如何打开命令行？**
*   **Windows:** 搜索 "Command Prompt" 或 "PowerShell"。
*   **macOS:** 搜索 "Terminal"。
*   **Linux:** 通常使用 Ctrl+Alt+T 快捷键打开终端。
*   **VS Code:** 内置终端 (View > Terminal 或 Ctrl+` )。
*   **JetBrains IDEs (如 IntelliJ IDEA, Android Studio):** 内置终端 (View > Tool Windows > Terminal 或 Alt+F12)。

### 1.2 什么是命令行中的命令

命令是在命令行中输入的特定文本字符串，用于指示计算机执行特定任务。例如，`git status` 就是一个命令，它告诉 Git 工具显示当前项目的状态。

### 1.3 认识 命令行 命令的基本结构

一个典型的命令行命令通常包含以下部分：

`命令名称 [选项] [参数]`

*   **命令名称 (Command Name):** 指定要执行的程序或工具，例如 `git`、`ls` (列出文件)、`cd` (改变目录)。
*   **选项 (Options/Flags):** 修改命令的行为。选项通常以一个或两个连字符开头，例如 `-a` 或 `--all`。
    *   `git commit -m "Initial commit"` 中的 `-m` 就是一个选项，表示后面跟着的是提交信息。
*   **参数 (Arguments):** 命令操作的对象，例如文件名、目录路径或URL。
    *   `git add README.md` 中的 `README.md` 就是一个参数，指定要添加到暂存区的文件。

**示例：**
*   `ls -l /home/user/documents`
    *   `ls`: 命令名称 (列出目录内容)
    *   `-l`: 选项 (以长格式列出)
    *   `/home/user/documents`: 参数 (要列出内容的目录路径)

### 1.4 学会使用 git 命令行工具

Git 是一个强大的分布式版本控制系统。以下是一些核心的 Git 命令，用于在本地管理你的项目。

**A. 初始化仓库与基本配置**

1.  **配置用户信息 (首次使用 Git 时必须配置)**
    ```bash
    git config --global user.name "Your Name"
    git config --global user.email "your.email@example.com"
    ```
    这些信息会出现在你的提交记录中。`--global` 表示这是全局配置，适用于你在这台电脑上的所有 Git 仓库。

2.  **初始化新仓库**
    进入你的项目文件夹，然后运行：
    ```bash
    cd /path/to/your/project
    git init
    ```
    这会在当前目录下创建一个名为 `.git` 的隐藏子目录，用于存储 Git 仓库的所有信息。

**B. 基本工作流程**

你的本地仓库有三个主要区域：
*   **工作目录 (Working Directory):** 你实际修改文件的区域。
*   **暂存区 (Staging Area / Index):** 一个临时区域，用于存放你希望在下一次提交中包含的更改。
*   **本地仓库 (Local Repository / .git directory):** 永久存储项目历史记录的地方。

基本流程是：在工作目录修改文件 -> 将修改添加到暂存区 -> 将暂存区的内容提交到本地仓库。

1.  **查看仓库状态**
    ```bash
    git status
    ```
    这个命令非常重要，它会告诉你当前分支、哪些文件被修改了、哪些文件在暂存区等。

2.  **将文件添加到暂存区**
    *   添加特定文件：
        ```bash
        git add <filename>
        # 例如: git add README.md
        ```
    *   添加多个文件：
        ```bash
        git add <file1> <file2>
        ```
    *   添加当前目录下所有已修改或新增的文件 (不包括被 `.gitignore` 忽略的文件)：
        ```bash
        git add .
        ```

3.  **提交更改到本地仓库**
    ```bash
    git commit -m "Your descriptive commit message"
    ```
    `-m` 选项允许你直接在命令行中提供提交信息。提交信息应该清晰、简洁地描述你所做的更改。参考前面链接的《Git Commit 之道》。

4.  **查看提交历史**
    ```bash
    git log
    ```
    *   查看简化的历史：
        ```bash
        git log --oneline
        ```
    *   查看历史并显示分支图：
        ```bash
        git log --oneline --graph --decorate --all
        ```

**C. 分支管理**

分支允许你独立于主线（通常是 `main` 或 `master` 分支）进行开发，而不会影响主线的稳定性。

1.  **查看所有本地分支**
    ```bash
    git branch
    ```
    当前活动分支会用 `*` 标记。

2.  **创建新分支**
    ```bash
    git branch <branch-name>
    # 例如: git branch feature-login
    ```

3.  **切换到分支**
    ```bash
    git checkout <branch-name>
    # 例如: git checkout feature-login
    ```
    或者，创建并立即切换到新分支：
    ```bash
    git checkout -b <new-branch-name>
    # 例如: git checkout -b feature-user-profile
    ```

4.  **合并分支**
    首先，切换到你想要合并入的目标分支（例如 `main`），然后合并其他分支的更改：
    ```bash
    git checkout main
    git merge <branch-to-merge>
    # 例如: git merge feature-login
    ```
    如果出现合并冲突，Git 会提示你，你需要手动解决冲突，然后再次提交。

5.  **删除分支 (在合并后)**
    ```bash
    git branch -d <branch-name>
    # 例如: git branch -d feature-login
    ```
    如果分支有没有被合并的更改，使用 `-D` 强制删除：
    ```bash
    git branch -D <branch-name>
    ```

**D. 标签管理**

标签通常用于标记项目的重要版本点，如 `v1.0`。

1.  **创建标签**
    *   创建一个轻量标签：
        ```bash
        git tag <tag-name>
        # 例如: git tag v1.0
        ```
    *   创建一个附注标签 (包含更多信息，推荐)：
        ```bash
        git tag -a <tag-name> -m "Tag message"
        # 例如: git tag -a v1.0 -m "Version 1.0 release"
        ```
    默认情况下，标签会打在最新的提交上。你也可以给过去的某个提交打标签：
    ```bash
    git log --oneline # 找到commit_hash
    git tag -a v0.9 <commit_hash> -m "Version 0.9 release"
    ```

2.  **查看标签**
    ```bash
    git tag
    ```

3.  **删除标签**
    ```bash
    git tag -d <tag-name>
    ```

### 1.5 学会使用vscode 自带的图形化界面进行仓库管理

Visual Studio Code (VS Code) 内置了强大的 Git 支持，提供了一个图形化界面来执行许多常见的 Git 操作。

1.  **打开源代码管理视图：** 点击左侧活动栏的源代码管理图标 (通常像一个分叉的树枝)，或者使用快捷键 `Ctrl+Shift+G`。
2.  **初始化仓库：** 如果你的项目尚未初始化为 Git 仓库，VS Code 会提示你 "Initialize Repository"。
3.  **查看更改：** 修改过的文件会列在 "Changes" 部分。
4.  **暂存更改：** 点击文件旁边的 `+` 号 (Stage Changes)。
5.  **提交更改：** 在顶部的输入框中输入提交信息，然后点击对勾 ✔️ (Commit) 按钮。
6.  **分支操作：** 点击左下角的状态栏中的分支名称，可以进行创建分支、切换分支等操作。
7.  **更多操作：** 点击源代码管理视图顶部的 `...` (更多操作) 按钮，可以找到拉取、推送、克隆、查看历史等更多 Git 功能。

虽然图形界面很方便，但理解命令行操作能帮助你更好地理解背后发生的事情，并在图形界面无法满足需求时提供解决方案。

### 1.6 学会使用 Android Studio 自带的图形化界面进行仓库管理

Android Studio (以及其他 JetBrains IDEs 如 IntelliJ IDEA) 同样深度集成了 Git。

1.  **启用版本控制：** 如果项目未启用，可以通过 `VCS > Enable Version Control Integration...` 并选择 Git。
2.  **Commit 工具窗口：** 通常在左侧或底部 (`View > Tool Windows > Commit` 或 `Alt+0` / `Cmd+0`)。这里会显示未暂存 (Unversioned Files, Changes) 和已暂存 (Staged) 的更改。你可以勾选文件，输入提交信息并提交。
3.  **Git 工具窗口：** 通常在底部 (`View > Tool Windows > Git` 或 `Alt+9` / `Cmd+9`)。这里有 `Log` 标签页，可以查看提交历史、分支图等。
4.  **分支操作：** IDE 右下角通常会显示当前分支名称，点击它可以进行分支的创建、切换、合并、删除等操作。
5.  **常用操作：**
    *   **Commit:** `Ctrl+K` (Windows/Linux) / `Cmd+K` (macOS)
    *   **Push:** `Ctrl+Shift+K` (Windows/Linux) / `Cmd+Shift+K` (macOS)
    *   **Update Project (Pull):** `Ctrl+T` (Windows/Linux) / `Cmd+T` (macOS)
    *   右键点击项目、目录或文件，在上下文菜单中通常有 `Git` 子菜单，包含各种 Git 操作。

## 2 学习使用命令行进行项目云端仓库的管理

本地仓库主要用于个人版本管理。当需要与他人协作或备份代码时，就需要使用远程仓库。

### 2.1 什么是git 远程仓库

Git 远程仓库是托管在网络服务器上的项目版本库。团队成员可以从远程仓库获取最新代码，并将自己的更改推送上去，从而实现协作。

常见的 Git 远程仓库托管服务有：
*   **GitHub:** 全球最大的代码托管平台，非常适合开源项目和个人项目。
*   **GitLab:** 功能全面的 DevOps 平台，提供从代码托管到 CI/CD 的完整解决方案，可以自建服务器。
*   **Gitee (码云):** 中国本土的代码托管平台，访问速度在国内较快。
*   **Bitbucket:** Atlassian 公司提供的代码托管服务，与 Jira 等产品集成良好。

你需要先在这些平台上创建一个账户，并创建一个新的空仓库。

### 2.2 如何将本地仓库关联到远程仓库

1.  **获取远程仓库 URL:**
    在你的远程仓库页面 (如 GitHub)，你会找到一个 URL，通常以 `https://` 或 `git@` 开头。例如 `https://github.com/your-username/your-repository.git`。

2.  **在本地仓库添加远程仓库地址:**
    打开命令行，进入你的本地项目目录，然后运行：
    ```bash
    git remote add <remote-name> <remote-repository-url>
    ```
    通常，我们将主要的远程仓库命名为 `origin`：
    ```bash
    git remote add origin https://github.com/your-username/your-repository.git
    ```

3.  **验证远程仓库是否添加成功:**
    ```bash
    git remote -v
    ```
    这会列出所有已配置的远程仓库及其 URL。你应该能看到类似：
    ```
    origin  https://github.com/your-username/your-repository.git (fetch)
    origin  https://github.com/your-username/your-repository.git (push)
    ```

### 2.3 如何将本地修改与远程仓库同步

将本地提交推送到远程仓库，以便其他人可以看到你的更改。

1.  **推送本地分支到远程仓库:**
    ```bash
    git push <remote-name> <local-branch-name>
    # 例如，推送本地 main 分支到 origin 远程仓库
    git push origin main
    ```
    如果是第一次推送一个新创建的本地分支，你可能需要设置上游分支：
    ```bash
    git push -u origin <local-branch-name>
    # 例如: git push -u origin feature-login
    ```
    `-u` (或 `--set-upstream`) 选项会将本地分支与远程分支关联起来。之后，你只需要运行 `git push` 即可推送到关联的远程分支。

    **注意:** 在推送前，最好先拉取远程仓库的最新更改，以避免冲突。

### 2.4 如何获取远程仓库别人上传的更改

从远程仓库获取最新的代码和提交历史。

1.  **获取远程仓库的更新 (但不合并):**
    ```bash
    git fetch <remote-name>
    # 例如: git fetch origin
    ```
    `git fetch` 会将远程仓库的最新数据下载到你的本地 `.git/refs/remotes/origin/` 目录下，但它不会自动修改你的工作目录或当前分支。你可以通过 `git log origin/main` 查看远程 `main` 分支的提交历史。

2.  **拉取远程仓库的更新 (获取并尝试合并):**
    ```bash
    git pull <remote-name> <remote-branch-name>
    # 例如，拉取 origin 远程仓库的 main 分支并合并到当前本地分支
    git pull origin main
    ```
    `git pull` 实际上是 `git fetch` 和 `git merge` (或 `git rebase`，取决于配置) 两个命令的组合。它会获取远程分支的更新，并尝试将其合并到你当前的本地分支。

    如果当前本地分支已经通过 `git push -u` 或 `git branch --set-upstream-to` 与远程分支关联，你可以简化为：
    ```bash
    git pull
    ```

    **处理冲突：** 如果 `git pull` 时，你的本地更改与远程更改有冲突，Git 会提示你合并冲突。你需要手动解决这些冲突，然后提交解决后的文件。

### 学习本地仓库进行版本管理 (JetBrains IDE 实战)

这一部分将重点介绍如何在 JetBrains IDEs (如 IntelliJ IDEA, Android Studio, PyCharm, WebStorm 等) 中使用其强大的图形化界面进行高效的本地版本管理。这些 IDE 提供了与 Git 的深度集成。

- **在 JetBrains IDE 中初始化 Git 仓库**
    1.  打开你的项目。
    2.  如果项目尚未进行版本控制，可以通过顶部菜单 `VCS > Enable Version Control Integration...`。
    3.  在弹出的对话框中，选择 `Git` 作为版本控制系统，然后点击 `OK`。
    4.  IDE 会在项目根目录下创建 `.git` 文件夹，并自动检测项目中的文件。

- **理解 IDE 中的暂存区 (Staging Area / Changelists)**
    JetBrains IDEs 使用 "Changelists" (变更列表) 的概念，这与 Git 的暂存区紧密相关。
    1.  打开 `Commit` 工具窗口 (通常在左侧边栏，或 `View > Tool Windows > Commit`，快捷键 `Alt+0` 或 `Cmd+0`)。
    2.  你会看到一个名为 "Changes" (或 "Default Changelist") 的列表，其中包含了所有已修改但尚未提交的文件。
    3.  **暂存更改：**
        *   **默认行为：** 较新版本的 IDE 可能默认不显式区分暂存区，而是直接提交选中的文件。
        *   **启用暂存区：** 如果你想使用明确的暂存区，可以在 `Commit` 工具窗口的设置中 (齿轮图标 ⚙️) 勾选 "Use Staging Area"。启用后，你会看到 "Unstaged" 和 "Staged" 两个区域。
        *   将文件从 "Unstaged" 拖到 "Staged"，或者右键点击文件选择 "Stage"。

- **提交更改 (Commit) 与查看历史 (Log)**
    - **如何使用 IDE 的提交界面:**
        1.  在 `Commit` 工具窗口中，勾选你想要提交的文件 (如果启用了暂存区，确保它们在 "Staged" 区域)。
        2.  在下方的 "Commit Message" 文本框中输入规范的提交信息。
        3.  点击 `Commit` 按钮 (或 `Commit and Push...` 直接提交并推送)。
    - **编写规范的提交信息:**
        *   **主题行 (Subject Line):** 简明扼要地概括更改内容，通常使用祈使句，例如 "Fix login button bug" 或 "Add user registration feature"。
        *   **正文 (Body - 可选):** 如果需要，空一行后可以写更详细的描述，解释为什么进行此更改，以及更改的影响。
        *   可以参考前面链接的《Git Commit 之道：规范化 Commit Message 写作指南》。
    - **通过 IDE 查看提交历史、分支图:**
        1.  打开 `Git` 工具窗口 (通常在底部工具栏，或 `View > Tool Windows > Git`，快捷键 `Alt+9` 或 `Cmd+9`)。
        2.  切换到 `Log` 标签页。
        3.  这里会显示项目的提交历史，包括作者、日期、提交信息，以及一个可视化的分支图。
        4.  你可以点击某个提交查看其详细信息和更改的文件。
        5.  可以使用顶部的筛选器按分支、用户、日期或内容进行筛选。

- **分支管理 (Branching)**
    - **在 IDE 中创建、切换、合并和删除分支:**
        1.  IDE 的右下角状态栏通常会显示当前 Git 分支的名称 (例如 `main` 或 `master`)。
        2.  点击该分支名称，会弹出一个 Git 分支操作的浮动窗口。
        3.  **创建新分支:** 点击 `+ New Branch`，输入新分支的名称，选择是否检出 (Checkout) 该分支，然后点击 `Create`。
        4.  **切换分支 (Checkout):** 在分支列表中，选择你想要切换到的本地分支或远程分支，然后点击 `Checkout`。
        5.  **合并分支:**
            *   首先，确保你当前所在的分支是你希望将更改合并**入**的分支 (例如，切换到 `main` 分支)。
            *   然后，在分支列表中选择你想要合并**来源**的分支 (例如 `feature-login`)，点击它，然后选择 `Merge into Current`。
            *   如果出现冲突，IDE 会弹出合并冲突解决工具。
        6.  **删除分支:** 在分支列表中，选择你想要删除的本地分支，点击它，然后选择 `Delete`。如果分支有未合并的更改，IDE 会警告你。

- **标签管理 (Tagging)**
    - **在 IDE 中创建和推送标签:**
        1.  打开 `Git Log` 视图。
        2.  右键点击你想要打标签的那个提交记录。
        3.  在上下文菜单中选择 `New Tag...`。
        4.  输入标签名称 (例如 `v1.0.0`)，可以选择添加一个标签信息 (Message)，然后点击 `Create Tag`。
        5.  **推送标签到远程仓库:** 默认情况下，`git push` 不会推送标签。你需要：
            *   通过菜单 `Git > Push...` (或 `Ctrl+Shift+K` / `Cmd+Shift+K`)。
            *   在 Push 对话框中，确保勾选了 `Push tags` 选项 (可能默认是 `All` 或需要手动选择 `Tags`)，或者点击配置按钮选择要推送的标签，然后点击 `Push`。
            *   或者，在 `Git Log` 中右键点击标签，选择 `Push Tag <tag-name>...`。

### 学习使用远程仓库进行协作并处理冲突 (JetBrains IDE 实战)

本节将指导你如何使用 JetBrains IDE 与远程仓库（如 GitHub, GitLab）进行交互，实现团队协作，并学习如何解决常见的代码冲突。

- **连接到远程仓库**
    - **在 IDE 中克隆 (Clone) 远程仓库:**
        1.  如果你是第一次获取项目，或者想在本地创建项目的副本：
        2.  在 IDE 的欢迎界面选择 `Get from VCS` (Version Control System)。
        3.  或者，如果已打开一个项目，通过菜单 `Git > Clone...` (或 `File > New > Project from Version Control...`)。
        4.  在 `URL` 字段粘贴远程仓库的 URL (例如 `https://github.com/user/repo.git`)。
        5.  选择本地存储的 `Directory`。
        6.  点击 `Clone`。IDE 会下载项目并在新窗口中打开。
    - **在 IDE 中添加远程仓库 (Remotes):**
        如果你的本地项目已经存在，但尚未关联远程仓库，或者需要添加多个远程仓库：
        1.  通过菜单 `Git > Manage Remotes...`。
        2.  在弹出的对话框中，点击 `+` 号。
        3.  输入远程仓库的名称 (通常是 `origin`) 和 URL。
        4.  点击 `OK`。

- **基本的远程操作**
    - **推送 (Push)：将本地提交推送到远程仓库**
        1.  在你本地进行了一些提交 (`Commit`) 之后。
        2.  通过菜单 `Git > Push...` (快捷键 `Ctrl+Shift+K` / `Cmd+Shift+K`)。
        3.  IDE 会显示一个对话框，列出本地分支及其将要推送到远程分支的更改。
        4.  你可以预览将要推送的提交。
        5.  点击 `Push`。如果远程分支有你本地没有的更新，推送可能会被拒绝，此时你需要先拉取更新。
    - **拉取 (Pull)：从远程仓库获取最新更改并合并**
        1.  通过菜单 `Git > Pull...` (或者工具栏上的更新项目图标，通常是向下箭头，快捷键 `Ctrl+T` / `Cmd+T`)。
        2.  在 Pull 对话框中，IDE 通常会自动选择当前分支对应的远程跟踪分支。
        3.  **Merge vs Rebase:** 你可以选择更新策略。
            *   **Merge (默认):** 会创建一个新的合并提交来整合远程更改。这会保留分支的完整历史。
            *   **Rebase:** 会将你的本地提交“变基”到远程分支的最新提交之后，使得提交历史更线性、更整洁。对于初学者，`Merge` 通常更安全直接。
        4.  点击 `Pull`。如果发生冲突，IDE 会提示你解决。
    - **获取 (Fetch)：从远程仓库获取最新更改但不合并**
        1.  通过菜单 `Git > Fetch`。
        2.  这会下载远程仓库的所有分支和标签的最新信息到你的本地 `origin/branch-name` 这样的远程跟踪分支，但不会修改你的本地工作分支。
        3.  之后你可以使用 `Git Log` 查看远程分支的更新，然后决定如何合并 (例如，手动执行 `Merge` 或 `Rebase`)。
        **Fetch 与 Pull 的区别:**
        *   `Fetch`: 只下载远程更新，不改变你的本地工作分支。你可以先看看远程有什么新东西。
        *   `Pull`: `Fetch` + `Merge` (或 `Rebase`)。下载并尝试自动合并到你的当前本地分支。

- **协作工作流 (以 Feature Branch Workflow 为例)**
    这是一种常见的协作模式：为每个新功能或修复创建一个独立的分支，完成后再合并回主开发分支 (如 `develop` 或 `main`)。
    - **创建和推送特性分支：**
        1.  在 IDE 右下角点击当前分支名，选择 `+ New Branch`，输入特性分支名 (例如 `feature/user-login` 或 `bugfix/issue-123`)，并确保 `Checkout branch` 被选中。
        2.  在该分支上进行开发和提交。
        3.  完成后，通过 `Git > Push...` 将这个新分支推送到远程仓库。勾选你的特性分支，IDE 可能会提示你此分支在远程不存在，并询问是否创建。
    - **团队成员间的代码同步：**
        *   **定期拉取主分支更新：** 在你的特性分支上工作时，主开发分支 (如 `develop` 或 `main`) 可能已经被其他团队成员更新。你需要定期将这些更新合并到你的特性分支，以尽早发现和解决冲突。
            1.  `Git > Fetch` 获取所有远程更新。
            2.  切换到你的特性分支 (`git checkout feature-user-login`)。
            3.  通过 `Git > Merge...` 或右键点击 `Log` 中的远程主分支 (`origin/develop`) 选择 `Merge into Current`，将主分支的更新合并到你的特性分支。或者使用 `Rebase` (见下文)。
        *   **或者，先更新本地主分支，再 rebase 特性分支：**
            1.  `git checkout develop`
            2.  `git pull origin develop`
            3.  `git checkout feature-user-login`
            4.  `git rebase develop` (这会将你的特性分支的提交应用在更新后的 `develop` 分支之上)
    - **发起合并请求 (Pull Request / Merge Request)：**
        *   当你的特性分支开发完成并通过测试后，通常会在代码托管平台 (如 GitHub, GitLab) 上创建一个 Pull Request (PR) 或 Merge Request (MR)。这是一个请求，要求项目维护者审查你的代码并将你的特性分支合并到主分支。
        *   **IDE 的作用：** IDE 本身不直接创建 PR/MR (除非有特定插件，如 GitHub 插件)，但你可以用 IDE 确保你的特性分支是干净的、最新的，并且已经推送到远程。
        *   **审查他人的 PR/MR:**
            1.  在 GitHub/GitLab 上找到 PR/MR，通常会显示其源分支名称 (例如 `someuser:feature-branch`)。
            2.  在 IDE 中，`Git > Fetch` 获取所有远程更新。
            3.  点击右下角分支名，在远程分支列表中找到该 PR/MR 对应的分支 (例如 `remotes/origin/someuser/feature-branch` 或 `remotes/pull/123/head` 对于 GitHub PRs)，选择 `Checkout`。这样你就可以在本地检出并测试该 PR 的代码了。

- **处理合并冲突 (Conflict Resolution)**
    - **冲突是如何产生的:** 当两个不同的分支修改了同一个文件的同一部分，并且 Git 无法自动决定哪个修改是正确的时，就会发生合并冲突。这在 `git pull`、`git merge` 或 `git rebase` 时都可能发生。
    - **使用 JetBrains IDE 的三方合并工具：**
        1.  当发生冲突时，IDE 会在 `Commit` 工具窗口或一个专门的 `Merge Conflicts` 对话框中列出冲突的文件。这些文件通常会标记为红色。
        2.  双击冲突文件，或选中后点击 `Resolve` (或右键选择 `Git > Resolve Conflicts...`)，会打开 IDE 的三方合并工具。
        3.  **合并工具界面：**
            *   **左侧面板 (Your version / Local changes):** 显示你当前分支的更改。
            *   **右侧面板 (Their version / Server changes / Changes from server):** 显示你正在合并进来的分支的更改。
            *   **中间面板 (Result):** 这是最终合并结果的预览。你需要在这里编辑以解决冲突。
        4.  **解决冲突：**
            *   对于每一处冲突的代码块 (高亮显示)，IDE 会提供箭头按钮 (`>>` 接受对方的, `<<` 接受你的) 或 `X` (拒绝某一方的)。
            *   你可以选择接受某一方的全部更改，或者手动编辑中间面板的代码，结合双方的更改。
            *   目标是让中间面板的代码是你期望的最终结果。
        5.  解决完一个文件中的所有冲突后，点击 `Apply` (或 `Accept Merge`)。
    - **提交解决冲突后的代码:**
        1.  当所有冲突文件都解决完毕后，它们会从冲突状态变回普通已修改状态。
        2.  在 `Commit` 工具窗口中，这些已解决的文件会被自动暂存 (或你可以手动暂存)。
        3.  编写一个提交信息 (例如 "Merge branch 'feature-login', resolving conflicts") 并 `Commit`。

- **其他有用的协作功能**
    - **储藏 (Stash)：在 IDE 中临时保存未完成的更改。**
        *   **场景：** 你正在开发一个功能，但突然需要切换到另一个分支修复一个紧急 bug，而当前工作目录的更改尚未完成，不想提交。
        *   **操作：**
            1.  `Git > Uncommitted Changes > Stash Changes...` (或右键项目 > Git > Uncommitted Changes > Stash Changes...)
            2.  给这个储藏起一个描述性的名字。
            3.  点击 `Create Stash`。你的工作目录会恢复到上一个提交的状态。
        *   **恢复储藏：**
            1.  `Git > Uncommitted Changes > Unstash Changes...`
            2.  选择要恢复的储藏，点击 `Apply Stash` (应用并保留储藏) 或 `Pop Stash` (应用并删除储藏)。
    - **拣选 (Cherry-pick)：在 IDE 中选择性地将某些提交应用到当前分支。**
        *   **场景：** 另一个分支上的某个特定提交修复了一个 bug，你希望将这个修复应用到当前分支，而不是合并整个分支。
        *   **操作：**
            1.  在 `Git Log` 视图中，找到你想要拣选的那个提交。
            2.  右键点击该提交，选择 `Cherry-Pick`。
            3.  该提交的更改会被应用到你当前的分支，并创建一个新的提交。
    - **变基 (Rebase)：在 IDE 中使用 Rebase 功能保持提交历史的整洁（特别是与远程主分支同步时）。**
        *   **场景：** 你在特性分支 `feature-A` 上开发，同时主分支 `main` 有了新的提交。你想让 `feature-A` 的历史看起来像是基于最新的 `main` 分支开发的，而不是有一个合并提交。
        *   **操作 (交互式 Rebase 更强大，但基础 Rebase 如下):**
            1.  确保你的工作目录是干净的 (提交或储藏所有更改)。
            2.  切换到你的特性分支: `git checkout feature-A` (在 IDE 右下角操作)。
            3.  `Git > Rebase...`
            4.  在对话框中，选择 `Onto` (或 `Onto branch`) 为 `main` (或你想要变基到的目标分支)。
            5.  点击 `Start Rebasing`。
            6.  如果发生冲突，IDE 会引导你逐个解决，解决后点击 `Continue Rebase`。
        *   **警告：** **不要对已经推送到共享远程仓库并被他人使用的分支执行 Rebase**，因为这会改写提交历史，给其他人造成困扰。通常只在本地私有分支或合并到主分支前整理特性分支时使用。

### 常见协作问题与 JetBrains IDE 解决方案

- **推送被拒绝 (Push Rejected) 如何处理等。**
    *   **原因：** 当你尝试 `git push` 时，如果远程分支包含了你本地没有的提交 (即其他人已经推送了新的更改)，你的推送会被拒绝，以防止覆盖他人的工作。
    *   **IDE 中的表现：** Push 对话框会显示 "Push rejected" 或类似错误信息。
    *   **解决方案：**
        1.  **首先拉取 (Pull) 远程更改：**
            *   点击 Push 对话框中的 `Merge` 或 `Rebase` 按钮 (如果有)，或者关闭对话框，执行 `Git > Pull...` (`Ctrl+T` / `Cmd+T`)。
            *   选择合并策略 (Merge 或 Rebase)。Merge 通常更简单直接。
        2.  **解决冲突 (如果发生)：** 如果拉取过程中发生合并冲突，使用 IDE 的三方合并工具解决它们，然后提交解决后的文件。
        3.  **再次推送 (Push)：** 冲突解决并提交后，再次尝试 `Git > Push...`。现在你的本地分支已经包含了远程的最新更改，推送应该会成功。
    *   **黄金法则：** 在推送前，养成先拉取 (或至少 Fetch 查看) 的好习惯。

## 学习在vscode 中使用自带源代码管理界面进行项目管理

VS Code 提供了简洁易用的源代码管理界面，非常适合日常的 Git 操作。

1.  **打开源代码管理视图 (Source Control View):**
    *   点击 VS Code 左侧活动栏中的分叉图标 (通常是第三个或第四个图标)。
    *   或者使用快捷键 `Ctrl+Shift+G`。

2.  **初始化仓库 (Initialize Repository):**
    *   如果你的项目文件夹还不是一个 Git 仓库，此视图会显示一个 "Initialize Repository" 按钮。点击它，VS Code 就会在当前项目根目录执行 `git init`。

3.  **查看和暂存更改 (Viewing and Staging Changes):**
    *   **Changes:** 当你修改了项目中的文件，这些文件会出现在 "Changes" 列表中。
    *   **Stage Changes:** 将鼠标悬停在文件名上，会出现一个 `+` (加号) 图标，点击它可以将该文件的更改添加到暂存区 (相当于 `git add <file>`)。
    *   **Stage All Changes:** "Changes" 标题栏旁边也有一个 `+` 图标，可以暂存所有已修改的文件。
    *   **Unstage Changes:** 对于已暂存的文件 (它们会移动到一个名为 "Staged Changes" 的区域，如果该视图模式开启的话，或者直接准备提交)，鼠标悬停时会出现一个 `-` (减号) 图标，点击它可以取消暂存 (相当于 `git reset HEAD <file>`)。

4.  **提交更改 (Committing Changes):**
    *   在源代码管理视图顶部的输入框中，输入你的提交信息 (Commit Message)。
    *   点击输入框上方的 ✔️ (对勾/Commit) 按钮。这会将所有已暂存的更改提交到本地仓库 (相当于 `git commit -m "your message"`)。
    *   **Commit All:** 如果你没有显式暂存任何文件，VS Code 可能会询问你是要提交所有更改还是仅提交特定文件。通常，点击 Commit 按钮会提交所有已跟踪文件的更改（除非你配置了只提交暂存文件）。

5.  **分支管理 (Branching):**
    *   **查看当前分支和切换分支:** VS Code 左下角状态栏会显示当前的分支名称。点击它可以打开一个命令面板，列出所有本地和远程分支。选择一个分支即可切换 (相当于 `git checkout <branch-name>`)。
    *   **创建新分支:** 在上述命令面板中，选择 `+ Create new branch...` 或 `+ Create new branch from...`。输入新分支的名称并回车。
    *   **删除分支:** 在分支列表中，找到要删除的分支，有时旁边会有删除图标，或者通过 Git 命令面板 (`Ctrl+Shift+P` 或 `Cmd+Shift+P`，输入 `Git: Delete Branch...`)。
    *   **合并分支:**
        1.  首先切换到你想要合并入的目标分支 (例如 `main`)。
        2.  打开命令面板 (`Ctrl+Shift+P` 或 `Cmd+Shift+P`)，输入 `Git: Merge Branch...`。
        3.  选择你想要合并的源分支。
        4.  如果出现冲突，VS Code 会标记冲突文件。

6.  **使用远程仓库 (Working with Remotes):**
    *   **克隆仓库 (Clone Repository):**
        1.  打开命令面板 (`Ctrl+Shift+P` 或 `Cmd+Shift+P`)，输入 `Git: Clone`。
        2.  粘贴远程仓库的 URL，按回车。
        3.  选择本地存储位置。
    *   **添加远程仓库 (Add Remote):**
        1.  打开命令面板，输入 `Git: Add Remote...`。
        2.  输入远程名称 (如 `origin`) 和 URL。
    *   **推送 (Push):**
        *   点击源代码管理视图中 `...` (更多操作) 菜单，选择 `Push`。
        *   或者，点击状态栏左下角同步图标旁边的向上箭头 (如果有待推送的提交)。
        *   如果本地分支没有设置上游分支，VS Code 会提示你发布该分支 (相当于 `git push -u origin <branch-name>`)。
    *   **拉取 (Pull):**
        *   点击 `...` 菜单，选择 `Pull`。这会获取远程更改并尝试合并到当前分支。
        *   或者，点击状态栏同步图标。
    *   **获取 (Fetch):**
        *   点击 `...` 菜单，选择 `Fetch`。这会下载远程更新但不会自动合并。
    *   **同步更改 (Sync / Synchronize Changes):**
        *   VS Code 状态栏左下角通常有一个同步图标 (两个循环箭头)。点击它可以执行 `git pull` 然后 `git push` (如果配置了默认行为)。它会尝试拉取远程更改，如果成功，再推送本地未推送的提交。

7.  **解决合并冲突 (Resolving Merge Conflicts):**
    *   当 `git pull` 或 `git merge` 导致冲突时，VS Code 会在源代码管理视图中将冲突文件标记出来。
    *   打开冲突文件，你会看到类似如下的标记：
        ```
        <<<<<<< HEAD (Current Change)
        // 你的本地更改
        =======
        // 远程或合并过来的更改
        >>>>>>> branch-name (Incoming Change)
        ```
    *   VS Code 会在这些冲突块上方提供可点击的操作：`Accept Current Change` | `Accept Incoming Change` | `Accept Both Changes` | `Compare Changes`。
    *   选择适当的操作，或者手动编辑代码以解决冲突。
    *   解决完一个文件中的所有冲突后，保存文件。
    *   然后通过源代码管理视图将解决后的文件暂存 (`+` 图标)。
    *   最后，提交这些已解决冲突的更改。

8.  **查看历史 (View History):**
    *   VS Code 没有像 JetBrains IDE 那样内置一个复杂的 Git Log 图形界面，但可以通过扩展来实现，例如 "GitLens" 或 "Git Graph"。
    *   GitLens (非常流行) 增强了内置的 Git 功能，可以查看文件或行的历史、比较提交等。
    *   你也可以在终端中使用 `git log` 命令。

通过结合使用 VS Code 的图形化界面和适时的命令行操作，你可以有效地进行版本控制。对于初学者，图形界面降低了入门门槛，而命令行的理解则能让你更深入地掌握 Git。
