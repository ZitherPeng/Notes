# GitHub笔记

### 一、git网站了解、仓库创建、设置
### 二、git工具

	#显示当前Git配置
	git config --list

	#设置提交仓库是的用户名信息
	git config --global user.name "username"

	#设置提交仓库是的邮箱信息
	git config --global user.email "xxxx@xxx.com"

### 三、git 命令

- **概念**：
```
Workspace: 工作区   #未被版本控制
Index/Stage:　暂存区 
Repository：仓库区（或本地仓库）
Remote: 远程仓库，例如github 、开源中国
```
- **命令**：	
  - 本地仓库命令
```	
	#在当前目录新建一个git代码库
	git init
	
	#下载一个项目和它的整个代码历史
	#URL格式： https://github.com/[username]/reposName
	git clone [url]
	
	#添加指定文件到暂存区
	git add [file1] [file2]
	
	#删除工作区文件,并将这次删除放入暂存区
	git rm [file1] [file2]
	
	#改名文件，并且将这个改名放入暂存区
	git mv [file-origin] [file-renamed]
	
	#提交暂存区到仓库
	git commit -m [message]
	
	#直接从工作区提交到仓库
	#前提该文件已经有仓库中的历史版本
	git commit -a -m [message]
	
	#显示变更信息
	git status
	
	#显示当前分支的历史版本
	git log
	git log --oneline #一行显示
	
	#查看某一个版本的变更信息
	git show [hashcode]
```

  - 远程仓库命令
```
	#增加远程仓库，并命名
	git remote add [shortname] [url]

	#将本地的提交推送到远程仓库
	git push [remote] [branch]

	#将远程仓库的提交拉下到本地
	git pull [remote] [branch]

	#查看git与那个远程仓库建立了连接
	git remote -v

	#在目录下直接clone 远程仓库
	git clone [url]
```

[在线练习GitHub命令: https://try.github.io](https://try.github.io)

