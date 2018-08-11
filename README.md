# git
learn git


1. git分布式版本控制系统
2. git add <file> 添加文件

    git commit -m <message> 提交添加内容的说明

    git status 掌握工作区的状态

    git diff 可以查看修改内容

    git log 或 git log --pretty=oneline 查看提交历史

    git reflog 查看命令历史

    版本回退：HEAD指向的版本就是当前版本 返回上个版本 git reset --hard  HEAD^

3. 暂存区

    把文件往Git版本库里添加的时候，是分两步执行的：
    第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区stage；
    第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支
4.  撤销修改

    场景1:当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

    场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，
    就回到了场景1，第二步按场景1操作。
5. 删除文件

   git rm <file> 文件文件

    git commit -m <message> 提交删除内容的说明

6. 分支管理
7. 创建与合并分支

    查看分支：git branch

    创建分支：git branch <name>

    切换分支：git checkout <name>

    创建+切换分支：git checkout -b <name> 

    比如创建切换分支dev：git checkout -b dev

    合并某分支到当前分支：git merge <name>

    删除分支：git branch -d <name>
8.  解决冲突

    分支的合并情况：git log --graph --pretty=oneline --abbrev-commit
9.  分支管理策略

    合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并

    git merge --no-ff -m "merge with no-ff" dev
10. bug分支

    修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
    当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场。
11. feature分支

    开发一个新feature，最好新建一个分支；
    如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。

12. 多人协作

    查看远程库信息，使用git remote -v；

    工作模式：

    1.首先，可以试图用git push origin <branch-name>推送自己的修改；

    2.如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

    3.如果合并有冲突，则解决冲突，并在本地提交；

    4.没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

    如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。

13. 创建标签：

    首先，切换到需要打标签的分支上
    git tag <name>就可以打一个新标签：git tag v0.1

    git tag查看所有标签

    git show <tagname>查看标签信息 比如git show v0.1

    创建带有说明的标签，用-a指定标签名，-m指定说明文字：
    git tag -a v0.1 -m "version 0.1 released" 1094adb

14. 操作标签：

    删除标签：git tag -d v0.1

    推送某个标签到远程，使用命令git push origin <tagname>: git push origin v0.1

    一次性推送全部尚未推送到远程的本地标签:git push origin --tags
    
    如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：git tag -d v0.9
    然后，从远程删除。删除命令也是push，但是格式如下：git push origin :refs/tags/v0.9