# Branch
---
1. 使用分支意味着你可以从开发主线上分离开来,然后在不影响主线的同时继续工作;
2. Git 中的分支实际上仅是一个包含所指对象校验和(40 个字符长度 SHA-1 字串)的文件,新建一个分支就是向一个文件写入 41 个字节(外加一个换行符),所以新建分支非常迅速；
3. Git 保存的不是文件差异或者变化量,而只是一系列文件快照;
4. 查看分支：
    * `git branch`;
    * 查看各个分支最后一次 commit 信息,运行`git branch -v`;
5. 创建一个新的分支: 
    * `git branch new_branch`;
    * 切换到新的分支：`git checkout new_branch`;
    * 新建分支并切换到该新分支：`git checkout -b new_branch`;
6. 合并分支：
    * 切换到你要合并的目地分支：`git checkout des_branch`;
    * 合并要合并的分支：`git merge src_branch`;
7. 快进（fast forward）：如果顺着一个分支走下去可以到达另一个分支,那么 Git 在合并两者时,只会简单地把指针前移；
8. 删除分支：
    * `git branch -d other_branch`;
    * 如果你修改了两个待合并分支里同一个文件的同一部分,Git 就无法干净地把两者合到一起;这时使用`git status`显示详细信息，然后人工解决该问题；
9. 查看哪些分支已被并入当前分支: `git branch --merged`;
10. 查看尚未合并的工作:  `git branch --no-merged`;
11. 推送数据: `git push origin your_branch:remote_branch_name`;
12. 把一个分支整合到另一个分支的办法有两种:
    * 合并（merge）;
    * 衍合（rebase）:在一个分支里提交的改变在另一个分支里重放一遍:
    <pre>
    git checkout test_branch
    git rebase master
    </pre>
    * `git rebase [main_branch] [test_branch]`
    * **永远不要衍合那些已经推送到公共仓库的更新**
