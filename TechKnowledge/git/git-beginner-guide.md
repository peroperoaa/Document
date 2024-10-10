# Git 零基础使用指南

## 1. Git 简介

Git 是一个分布式版本控制系统，用于跟踪文件的变化，并协调多人协作的软件开发。

## 2. Git 仓库介绍

Git 仓库（Repository）是项目的容器，包含了项目的所有文件和每个文件的修改历史。

### 仓库的类型：

1. **本地仓库**：存储在本地计算机上的仓库。
2. **远程仓库**：存储在远程服务器上的仓库，如 GitHub、GitLab 等。

## 3. Git 基础概念

### 3.1 工作区（Working Directory）

实际操作的目录，包含项目的所有文件。

### 3.2 暂存区（ Index）

一个中间区域，用于存放准备提交的修改。

### 3.3 本地仓库（Local Repository）

存储项目历史记录的地方。

### 3.4 远程仓库（Remote Repository）

存储在远程服务器上的仓库副本。

## 4. Git 基本工作流程

1. 在工作区修改文件
2. 将修改添加到暂存区
3. 将暂存区的修改提交到本地仓库
4. （可选）将本地仓库的修改推送到远程仓库

## 5. 安装 Git

- Windows：从 [git-scm.com](https://git-scm.com/) 下载安装程序
- macOS：使用 Homebrew 安装：`brew install git`
- Linux：使用包管理器安装，如 `sudo apt-get install git`

## 6. 基本配置

设置用户名和邮箱：

```
git config --global user.name "Your Name"
git config --global user.email "your_email@example.com"
```

## 7. 创建仓库

### 初始化新仓库：

```
git init
```

### 克隆现有仓库：

```
git clone https://github.com/example/repository.git
```

## 8. 基本操作

### 查看状态：

```
git status
```

### 添加文件到暂存区：

```cpp
git add <filename> //将filename同步到暂存区
git add . //将所有修改同步到暂存区
```

### 提交更改：

```cpp
git commit //进入默认编辑器(vi/vim)编辑提交信息
git commit -m "Commit message" // -m可直接编辑提交信息
```

### 查看提交历史：

```cpp
git log
git log --oneline //简略显示提交历史内容
```

### 版本回退：

1. `git reset --soft <版本ID>`:

   - 工作区：不发生变化，所有的修改保持原样。
   - 暂存区：不发生变化，之前暂存的内容保持不变。
   - 仓库：HEAD 指针移动到指定的提交，但不影响工作区和暂存区的内容。
   - [更多关于soft option的细节](./关于git reset --soft 的细节)

2. `git reset --mixed`（默认选项）:

   - 工作区：不发生变化，所有的修改保持原样。
   - 暂存区：被重置为与指定提交相匹配的状态。之前暂存的更改会被取消暂存，但仍保留在工作区中。
   - 仓库：HEAD 指针移动到指定的提交。

3. `git reset --hard`:

   ​	**谨慎使用**

   - 工作区：被完全重置为指定提交的状态。所有未提交的修改都会被丢弃。
   - 暂存区：被完全重置为指定提交的状态。所有暂存的更改都会被丢弃。
   - 仓库：HEAD 指针移动到指定的提交。

4. ``git reflog``:

   查看操作历史记录

### 查看差异：	

```cpp
git diff //默认展示工作区和暂存区差异
git diff HEAD //展示工作区和仓库的差异
git diff --cached //展示暂存区和仓库的差异
git diff <id1> <id2> //展示id1到id2版本的差异
git diff HEAD~<num> HEAD <file> //展示HEAD前第num个版本和HEAD版本中file的差异
```

### 删除文件：

```cpp
git rm <file> //删除工作区和暂存区的file文件(记得commit)
git rm --cached <file> //仅删除暂存区中的file文件
```

### **``.gitignore``文件:**

``.gitignore``生效的前提：目标文件不能不能是已被添加到版本库的文件

``.gitignore``文件中添加``temp/``可以忽略``.gitignore``任何路径下的``temp``文件夹





## 9. 分支操作

### 创建分支：

```
git branch branch_name
```

### 切换分支：

```
git checkout branch_name
```

### 合并分支：

```
git merge branch_name
```

## 10. 远程仓库操作

### 添加远程仓库：

```
git remote add origin https://github.com/username/repository.git
```

### 推送到远程仓库：

```
git push -u origin master
```

### 从远程仓库拉取：

```
git pull origin master
```

## 11. 常见问题和解决方法

1. **合并冲突**：当两个分支修改了同一文件的同一部分时发生。需要手动解决冲突。

2. **撤销提交**：使用 `git reset` 或 `git revert` 命令。

3. **找回已删除的文件**：使用 `git checkout` 恢复文件。

## 12. 进阶学习建议

- 学习更复杂的分支策略
- 了解 Git 钩子（Hooks）
- 探索 Git 工作流，如 Gitflow
- 学习使用图形化 Git 工具

记住，熟练使用 Git 需要时间和实践。不要害怕犯错，因为 Git 设计的初衷就是帮助你管理和恢复更改。

