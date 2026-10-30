# **GitLearning**
[Git](https://liaoxuefeng.com/books/git/introduction/index.html)
 is a version control system.
Git is free software.
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git tracks changes of files.
![photo](https://pic2.zhimg.com/v2-4f61dac0b425ebe34efc88d11a68f27b_1440w.jpg)
<hr>

## Commands
### **add**
   - `git add ""`
### **commit**
   - `git commit -m ""`
### **status**
   - `git status` for which file is modified.
### **diff**
   - `git diff ""` for specific details of the difference
### **log**
   - `git log --graph --pretty=oneline --abbrev-commit` 图形化显示分支
### **reset**
   - `git reset --hard HEAD^^` ^代表上一个版本, 
   - `--hard` 回退到上个版本已提交的状态
   - `--soft` 回退到上个版本未提交的状态
   - `--mixed` 回退到上个版本已添加但未提交的状态
   - `git reset HEAD <file>` 可以把暂存区的修改撤销(unstage), 重新放回工作区
### **checkout(其实就是用版本库里的版本替换工作区的版本, 无论修改还是删除)**
   - `git checkout -- README.md`
     - 自修改后未放入暂存区, 撤销修改回到和版本库一样的状态
     - 已经添加到暂存区后修改, 撤销后回到添加到暂存区的状态 
### **rm**
   - `rm <file>`(或手动删除) + `git rm <file>`(类似手动修改后 + `git add <file>`)
   - 删错了 `git checkout -- <file>` 版本库里还有, 直接恢复到最新版本(必须是曾添加到库里的文件; 会丢失最近一次提交后修改的内容(没有提交就删除))
### **remote**
   - `git remote add origin(远程库名字, 默认为origin) git@github.com:Frisius258/LearnGit.git`
   - `git remote` 查看远程库的信息
   - `git remote -v` 更详细的信息
### **push**
   - 每次本地提交后, 只要有必要, 就可以使用命令 `git push origin master` 推送最新修改
   - 分支是否推送取决于你和你的小伙伴是否需要共同在上面开发, 一般时刻推送 master 主分支和 dev 开发分支
### **branch**
   - `git branch` 列出所有分支
   - `git checkout -b <name>` 创建并切换到分支 `<name>`
   - `git checkout <name>` 切换到分支 `<name>`
   - `git merge <name>` 先切换回`master`分支, 然后合并 *(master)和 `<name>`(合并指定分支到当前分支)
   - `git merge --no-ff -m "merge with no-ff" dev` 强制禁用`Fast forward`模式, 可以在删除分支后的历史中看到分支的合并信息(这样会创建一个新的commit, 因此需要-m(commit 的 message参数)).
   - `git branch -d <name>` 合并完成后删除`<name>`分支
### **switch**
   - 更科学的切换分支方式
   - `git switch -c <name>` 创建并切换到新的分支 `<name>`
   - `git switch <name>` 切换到已有分支  
   - 解决冲突:
     - 当在同一节点的不同分支对相同文件都做了修改的时候, 这时会 `Merge conflict`
     - 分支管理: 实际开发中, master 分支应该非常稳定, 只在发布版本时变更；实际工作时都在`dev`分支上干活, 每个人都有自己的分支, 不时需要向`dev`合并
     - ![Image](https://liaoxuefeng.com/books/git/branch/policy/branches.png)
### **stash**
   - `git stash` 用于保存当前的工作现场并进入一个干净的临时工作区, 这时可以随意切换创建分支而不影响之前没有add和commit的代码
   - 修复完成后切换到`master`分支完成合并并删除修bug的分支
   - `git stash list` 查看之前的工作区被存到哪里了
   - `git stash apply` 恢复当时的工作现场, 其次使用 `git stash drop` 删除stash中的内容
   - `git stash pop` 恢复工作现场并删除stash内容
   - 在master分支上修复了bug后, 由于dev是修bug前从master分过来的, 可以使用`cherry-pick`命令修复同样的bug(不用再手动把修bug的代码复制过来了)
   - `git cherry-pick <commit>` `<commit>`(SHA1)代表修bug的这个提交所做的修改, 而不是把`master`分支merge过来(Git会自动给dev分支做一次提交)
### **feature**
   - 开发新功能的时候, 最后新建一个feature分支, 这样可以在最后不想要此功能时直接通过删除分支删除feature
   - `git branch -D <feature-name>` `-D` 会完全丢失修改
### **pull**
   - 先指定本地`dev`分支与远程`origin/dev`分支的链接
     `git branch --set-upstream-to=origin/dev dev`
   - `git pull` 指定链接后pull, 但merge有冲突, 需要本地手动解决
### **rebase**
   - 将Git分叉的提交历史整理成一条干净的直线(强迫症狂喜)
   - `git rebase`
### **tag**
   - 实质就是指向commit的SHA1 id的一个别名指针
   - `git switch`先切换到需要的分支
   - `git tag <name>` 创建一个新的tag
   - `git tag`查看已有的所有tag, tag是按字母排序的
   - `git tag <name>` 默认tag打在最新提交的commit上
   - `git show <tagname>` 可以查看标签的信息
   - 如果忘了给之前的版本打tag, 可以使用`log...-commit`找到历史提交的id
   - `git tag -a v0.1 -m "version 0.1 released" 1094adb` 创建带有说明的标签，用-a指定标签名，-m指定说明文字，使用`git show <tagname>` 可以看到说明文字
   - `git tag -d <tagname>` 删除打错的标签
   - `git push origin <tagname>` 将某个标签推送到远程
   - `git push origin --tags` 一次性推送全部尚未推送到远程的本地标签
   - 如果tag已经推送到远程, 删除会更麻烦
     - `git tag -d <tagname>` 先从本地删除
     - `git push origin :refs/tags/<tagname>` 从远程删除 `:...`的作用是提供了被删除的tag原先的位置, 让remote库发现这个更改并删除
### **[PULL request](https://liaoxuefeng.com/books/git/github/index.html)**
### **[.gitignore](https://liaoxuefeng.com/books/git/customize/ignore/index.html)**