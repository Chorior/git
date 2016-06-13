# Git Tools
---
1. 通常在一个项目中,使用八到十个字符来避免 SHA-1 歧义已经足够了。最大的 Git 项目之一,Linux 内核,目前也只需要最长 40 个字符中的 12 个字符来保持唯一性;
2. 查看引用日志: `git reflog`;
3. 查看仓库中 HEAD 在n次前的值: `git show HEAD@{n}`;
4. 查看类似于`git log`输出格式的引用日志信息: `git log -g master`;
5. 日志引用信息只存在于本地,新克隆一个仓库的时候,引用日志是空的;
6. * 在引用最后加上一个 `ˆ`,表示此次提交的父提交;
    * 在`ˆ`后添加一个数字n，表示此次提交的第n父提交，只在合并提交时才会存在多个父提交；
    * `HEAD~`也表示父提交；
    * 在`~`后添加一个数字n，如`HEAD~2`表示第一父提交的第一父提交,这个可以写为`HEADˆˆˆ`;
7. * 查看你的试验分支上哪些没有被提交到主分支: `git log master..experment`;
    * 在引用前使用 `ˆ`字符或者`--not`指明你不希望提交被包含其中的分支:
        <pre>
            git log refA..refB
            git log ^refA refB
            git log refB --not refA
        </pre>
    * 查找所有从`refA`或`refB`包含的但是不被`refC`包含的提交: `git log refA refB ^refC`;
    * 查看`master`或者`experiment`中包含的但不是两者共有的引用: `git log master...experiment`;
    * 显示每个提交到底处于哪一侧的分支: `git log --left-right master...experiment`;
8. 进入交互式暂存区: `git add -i`;
9. * 切换分支,不提交正在进行中的工作,往堆栈推送一个新的储藏: `git stash`;
    * 查看现有的储藏: `git stash list`;
    * 应用储藏: `git stash apply stash@n`;
    * 重新应用文件变更，同时重新应用被暂存的变更: `git stash apply --index`;
    * 移除储藏: `git stash drop stash@n`;
    * 从储藏中创建分支并丢弃储藏: `git stash branch new_branch`;
10. 提交后想修改被提交的快照,增加或者修改其中的文件:
    * 修改或者增加删除文件;
    * `git add`或者`git rm`;
    * `git commit --amend`;
11. 从所有提交中删除一个文件:
    * `git filter-branch --tree-filter 'rm -f passwords.txt' HEAD`;
12. 子模块；            
