# git 的使用

+ 使用思想，首先去github 克隆 一个项目到本地 为工作区  

  ```shell
  git clone (url) https://github.com/lqrDream/blog.git
  ```

  

+ 必须为本地库设置一个 用户和邮箱

  ```shell
  git config --global user.name "mvpbang" 
  git config --global user.email "123456789@qq.com"
  ```

  

+ 首先需要在本地完成一次本地库的上传

  ```shell
  git status 查看 文件状态 
  git add 添加上传文件   git add  * 添加所有文件
  git commit -m  "文件描述"  
  ```

  

+ 将本地文件库 上穿到 github 

  ```shell
  git push  
  ```

  

# 将本地项目上传到新的github库

+ 首先初始化文件

  ```shell
  git init	
  ```

  

+ 设置上传的文件 库 

  ```shell
  git remote add origin https://github.com/lqrDream/test.git
  ```

  

+ 提交到库

  ```shell
  git push origin master
  git push --set-upstream origin master 设置使记住相应的别名 和分支,  可以直接 git push 
  ```

  ### add
  
  ```shell
  git add * #跟踪新文件
  git add -u [path] #添加[指定路径下]已跟踪文件
  ```
  
  
  
  ### rm
  
  ```shell
  rm *&git rm * #移除文件
  git rm -f * #移除文件
  git rm --cached * #取消跟踪
  git mv file_from file_to #重命名跟踪文件
  git log #查看提交记录
  ```
  
  
  
  ### commit
  
  ```shell
  git commit #提交更新
  git commit -m 'message' #提交说明
  git commit -a #跳过使用暂存区域，把所有已经跟踪过的文件暂存起来一并提交
  git commit --amend #修改最后一次提交
  git commit log #查看所有提交，包括没有push的commit
  git commit -m "#133" #关联issue 任意位置带上# 符号加上issue号码
  git commit -m "fix #133" commit关闭issue
  git commit -m '概要描述'$'\n\n''1.详细描述'$'\n''2.详细描述' #提交简要描述和详细描述
  ```
  
  
  
  ### reset
  
  ```shell
  git reset HEAD *#取消已经暂存的文件
  git reset --mixed HEAD *#同上
  git reset --soft HEAD *#重置到指定状态，不会修改索引区和工作树
  git reset --hard HEAD *#重置到指定状态，会修改索引区和工作树
  git reset -- files *#重置index区文件
  那么如何跟随着commit关闭一个issue呢? 在confirm merge的时候可以使用一下命令来关闭相关issue:
  \1. fixes #xxx 1. fixed #xxx 1. fix #xxx 1. closes #xxx 1. close #xxx 1. closed #xxx
  ```
  
  
  
  ### revert
  
  ```sh
  git revert HEAD #撤销前一次操作
  git revert HEAD~ #撤销前前一次操作
  git revert commit ##撤销指定操作
  ```
  
  ### checkout
  
  ```shell
  git checkout -- file #取消对文件的修改（从暂存区——覆盖worktree file）
  git checkout branch|tag|commit -- file_name #从仓库取出file覆盖当前分支
  git checkout HEAD~1 [文件] #将会更新 working directory 去匹配某次 commit
  git checkout -- . #从暂存区取出文件覆盖工作区
  git checkout -b gh-pages 0c304c9 这个表示 从当前分支 commit 哈希值为 0c304c9 的节点，分一个新的分支gh-pages出来，并切换到 gh-pages
  ```
  
  
  
  ### diff
  
  ```shell
  git diff file #查看指定文件的差异
  git diff --stat #查看简单的diff结果
  git diff #比较Worktree和Index之间的差异
  git diff --cached #比较Index和HEAD之间的差异
  git diff HEAD #比较Worktree和HEAD之间的差异
  git diff branch #比较Worktree和branch之间的差异
  git diff branch1 branch2 #比较两次分支之间的差异
  git diff commit commit #比较两次提交之间的差异
  $ git diff master..test #上面这条命令只显示两个分支间的差异
  git diff master...test #你想找出‘master’,‘test’的共有 父分支和'test'分支之间的差异，你用3个‘.'来取代前面的两个'.'
  ```
  
  
  
  ### stash
  
  ```shell
  git stash #将工作区现场（已跟踪文件）储藏起来，等以后恢复后继续工作。
  git stash list #查看保存的工作现场
  git stash apply #恢复工作现场
  git stash drop #删除stash内容
  git stash pop #恢复的同时直接删除stash内容
  git stash apply stash@{0} #恢复指定的工作现场，当你保存了不只一份工作现场时。
  ```
  
  
  
  ### merge
  
  ```shell
  git merge --squash test ##合并压缩，将test上的commit压缩为一条
  ```
  
  
  
  ### cherry-pick
  
  ```shell
  git cherry-pick commit #拣选合并，将commit合并到当前分支
  git cherry-pick -n commit #拣选多个提交，合并完后可以继续拣选下一个提交
  ```
  
  
  
  ### rebase
  
  ```shell
  git rebase master #将master分之上超前的提交，变基到当前分支
  git rebase --onto master 169a6 #限制回滚范围，rebase当前分支从169a6以后的提交
  git rebase --interactive #交互模式，修改commit
  git rebase --continue #处理完冲突继续合并
  git rebase --skip #跳过
  git rebase --abort #取消合并
  ```
  
  
  
  ## 分支branch
  
  ### 删除
  
  ```shell
  git push origin :branchName #删除远程分支
  git push origin --delete new #删除远程分支new
  git branch -d branchName #删除本地分支，强制删除用-D
  git branch -d test #删除本地test分支
  git branch -D test #强制删除本地test分支
  ```
  
  
  
  ### 提交	
  
  ```shell
  git push -u origin branchName #提交分支到远程origin主机中
  ```
  
  
  
  ### 拉取
  
  ```shell
  git fetch -p #拉取远程分支时，自动清理 远程分支已删除，本地还存在的对应同名分支。
  ```
  
  
  
  ### 分支合并
  
  ```shell
  git merge branchName #合并分支 - 将分支branchName和当前所在分支合并
  git merge origin/master #在本地分支上合并远程分支。
  git rebase origin/master #在本地分支上合并远程分支。
  git merge test #将test分支合并到当前分支
  ```
  
  
  
  ### 查看分支日志
  
  ```shell
  git reflog查出要回退到merge之前的版本号
  git reflog 
  git reset --hard 版本号 回到合并之前的版本
  gitk  显示log面板
  ```
  
  
  
  ### 重命名
  
  ```shell
  git branch -m old new #重命名分支
  ```
  
  
  
  ### 查看
  
  ```shell
  git branch #列出本地分支
  git branch -r #列出远端分支
  git branch -a #列出所有分支
  git branch -v #查看各个分支最后一个提交对象的信息
  git branch --merge #查看已经合并到当前分支的分支
  git branch --no-merge #查看为合并到当前分支的分支
  ```
  
  
  
  ### 新建
  
  ```shell
  git branch test #新建test分支
  git checkout -b newBrach origin/master #取回远程主机的更新以后，在它的基础上创建一个新的分支
  ```
  
  
  
  ### 连接
  
  ```shell
  git branch --set-upstream dev origin/dev #将本地dev分支与远程dev分支之间建立链接
  git branch --set-upstream master origin/next #手动建立追踪关系
  ```
  
  
  
  ### 分支切换
  
  ```shell
  git checkout test #切换到test分支
  git checkout -b test #新建+切换到test分支
  git checkout -b test dev #基于dev新建test分支，并切换
  ```
  
  
  
  ## 远端
  
  ```shell
  git fetch <远程主机名> <分支名> #fetch取回所有分支（branch）的更新
  git fetch origin remotebranch[:localbranch] # 从远端拉去分支[到本地指定分支]
  git merge origin/branch #合并远端上指定分支
  git pull origin remotebranch:localbranch # 拉去远端分支到本地分支
  git push origin branch #将当前分支，推送到远端上指定分支
  git push origin localbranch:remotebranch #推送本地指定分支，到远端上指定分支
  git push origin :remotebranch #删除远端指定分支
  git checkout -b [--track] test origin/dev 基于远端dev分支，新建本地test分支[同时设置跟踪]
  ```
  
  
  
  ### 撤销远程记录
  
  ```shell
  git reset --hard HEAD~1 #撤销一条记录
  git push -f origin HEAD:master #同步到远程仓库
  ```
  
  
  
  ## 忽略文件
  
  ```shell
  echo node_modules/ >> .gitignore
  ```
  
  ## 删除文件
  
  ```shell
  git rm -rf node_modules/
  ```
  
  ## 源remote
  
  ```shell
  git是一个分布式代码管理工具，所以可以支持多个仓库，在git里，服务器上的仓库在本地称之为remote。
  个人开发时，多源用的可能不多，但多源其实非常有用。
  git remote add origin1 git@github.com:yanhaijing/data.js.git
  git remote #显示全部源
  git remote -v #显示全部源+详细信息
  git remote rename origin1 origin2 #重命名
  git remote rm origin #删除
  git remote show origin #查看指定源的全部信息
  ```
  
  