# Git简单命令使用总结
- ```git clone [url] ```
	从远程服务器上下载整个项目和代码提交记录到本地
	
- ```git clone [url] - - depth [num]```
	同上，拉取只有最近几条提交记录的完整代码
	> **注意：**由于.git/objects会默认保存每一次提交过的文件（即使已经废弃也会保存），所以服务器上的项目会越来越大，会最终导致clone失败，报错误：`error:RPC failed;curl 18 transfer closed with outstanding read data remaining`，用**上面命令**可解决
	
- ```git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*```
	配置fetch信息
	> **注意：**使用depth参数会导致 **查看不了远程分支**，是因为没有fetch过来。用 git fetch命令无效的情况下，是因为fetch配置路径不对，配置**上面命令**可解决。但关联的是所有分支信息，迭代次数多的情况下，可能会达到几G大小，显然没必要；只想关联想要的分支信息，每次修改fetch配置就可以。对应的**星号**改成**远程分支名称**。如：`git config remote.origin.fetch "+refs/heads/分支名:refs/remotes/origin/分支名`

- ```git config -- get remote.origin.fetch``
	查看fetch配置信息
- ```git status```
	显示当前有变更的文件
	
- ```git stash```
	备份当前的工作区的内容，从最近的一次提交中读取相关内容，让工作区保证和上次提交的内容一致。同时，将当前的工作区内容保存到Git栈中。**通俗的说就是，把上次提交以后到当前时间之间的所有内容暂时保存在Git栈内，保持当前代码与上一次提交后的代码一致，然后再pull代码，保证最近一段时间没有人提代码，防止比较难搞的冲突**
	
- ```git stash pop```
	从Git栈中读取最近一次保存的内容，恢复工作区内相关内容。**由于可能存在多个Stash的内容，所以用栈来管理，pop会从最近的一个stash中读取内容并恢复。**	

- ```git stash list```
	查看看Git栈内的所有备份

- ```git stash clear```
	清空Git栈内保存的所有备份

- ```git add [file]```

- ```git checkout```

- ```git commit```

- ```git push```

-----------------------------------
##分支相关
- ```git branch```
	查看本地分支

- ```git branch 分支名```
	创建本地分支，但不把指针切换到该分支下

- ```git branch -r```
	查看远程分支

- ```git branch -a```
	查看所有分支（本地+远程）

- ```git branch -m|-M old_branch new_branch```
   重命名分支，如果new_branch名字分支已经存在，则需要使用-M强制重命名，否则，使用-m进行重命名。

- ```git branch -d | -D branch_name```
   删除本地branch_name分支

- ```git branch -d -r branch_name```
    删除远程branch_name分支

- ```git checkout -b 本地分支名 origin/远程分支名```
    创建本地分支并与远程分支关联、并把指针切换到该本地分支下
    
