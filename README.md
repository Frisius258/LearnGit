# **GitLearning**
[Git](https://liaoxuefeng.com/books/git/introduction/index.html)
Git is a version control system.
Git is free software.
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git tracks changes of files.
![photo](https://pic2.zhimg.com/v2-4f61dac0b425ebe34efc88d11a68f27b_1440w.jpg)

### Commands
1. add
   `git add ""`
2. commit
   `git commit -m ""`
3. status
   `git status` for which file is modified.
4. diff
   `git diff ""` for specific details of the difference
5. reset
   - `git reset --hard HEAD^^` ^代表上一个版本, 
   - `--hard` 回退到上个版本已提交的状态
   - `--soft` 回退到上个版本未提交的状态
   - `--mixed` 回退到上个版本已添加但未提交的状态
   - `git reset HEAD <file>` 可以把暂存区的修改撤销(unstage), 重新放回工作区
6. checkout(其实就是用版本库里的版本替换工作区的版本, 无论修改还是删除)
   - `git checkout -- README.md`
     - 自修改后未放入暂存区, 撤销修改回到和版本库一样的状态
     - 已经添加到暂存区后修改, 撤销后回到添加到暂存区的状态 
7. rm
   - `rm <file>`(或手动删除) + `git rm <file>`(类似手动修改后 + `git add <file>`)
   - 删错了 `git checkout -- <file>` 版本库里还有, 直接恢复到最新版本(必须是曾添加到库里的文件; 会丢失最近一次提交后修改的内容(没有提交就删除))
8. remote
   - `git remote add origin(远程库名字, 默认为origin) git@github.com:Frisius258/LearnGit.git`
9. push
   - 每次本地提交后, 只要有必要, 就可以使用命令 `git push origin master` 推送最新修改
10. branch
   - `git branch` 列出所有分支
   - `git checkout -b <name>` 创建并切换到分支 `<name>`
   - `git checkout <name>` 切换到分支 `<name>`
   - `git merge <name>` 先切换回`master`分支, 然后合并 *(master)和 `<name>`(合并指定分支到当前分支)
   - `git branch -d <name>` 合并完成后删除`<name>`分支
11. switch
   - 更科学的切换分支方式
   - `git switch -c <name>` 创建并切换到新的分支 `<name>`
   - `git switch <name>` 切换到已有分支  
   - 解决冲突:
     - 当在同一节点的不同分支对相同文件都做了修改的时候, 这时会 `Merge conflict`
       - 分支测试1