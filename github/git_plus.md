# Git 进阶  

## Git简介
开源的分布式的版本管理系统。发明人 Linus Torvalds（Linux 创始人）。  
- 优势：
  - 便宜快速的本地分支
  - 所有内容都在本地端
  - Git 很快
  - Git 很省磁盘空间
  - Staging 功能
  - 它是分布的
  - 适用任何工作流程

### 版本控制
- 本地版本控制系统（无法协同工作）  
- 集中式的版本控制系统（中央服务器的单点故障）
- 分布式的版本控制系统

### Git 存储方式
- 传统版本控制系统存储方式(保留所有差异版本) 
![传统存储方式](./images/traditional_storage_mode.png)
- Git的存储方式（1.快照<gzip压缩>和指针 2.打包文件<存储文件和差异>）
![Git的存储方式](./images/git_storage_mode.png)  

### 三个区域
![](./images/three_part.png)
### 四种状态
Untracked 和 Modified 是工作区的两个状态。
![](./images/four_status.png)

## GUI工具  
- Git GUI
- Source Tree
- EGit(Eclipse插件)


**Git GUI**
启动图形界面历史记录（快捷键）
Git Bash 下命令： gitk

## Git 配置
### .gitignore
`# 后接注释`
![](./images/gitignore_use.png)
.gitignore 模板
GitHub 在新建仓时有一些模板，按语言分类。
<https://github.com/github/gitignore>
查看忽略规则 `git check-ignore -v .project`

### 换行符
![](./images/linefeed.png)

### 别名  
如：查看历史记录（图形形式）
```Bash
git log --pretty=format:'%h %ad | %s%d [%an]' --graph --date=short
哈希值 提交时间 | 提交信息 [提交人] --图形显示 --短日期
```
设置别名
```
git config --global alias.ci commit
将 commit 设置别名为 ci
```
```
cd ~ 到根目录下修改.gitconfig文件设置别名
cd - 回到仓库
```

