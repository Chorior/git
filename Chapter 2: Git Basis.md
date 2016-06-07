# Git basis
---
1. 两种取得 Git 项目仓库的方法：
    * 在现存的目录下，通过导入所有文件来创建新的Git仓库；
    * 从已有的Git仓库克隆出一个新的镜像仓库；
2. 对现有的某个项目开始用 Git 管理：`git init`;
3. 克隆仓库: 
    * 克隆我的git仓库：`git clone git://github.com/Chorior/git.git`；
    * 自定义新建项目目录名：`git clone git://github.com/Chorior/git.git pz_git`;
4. 工作目录下所有文件有且只有两种状态：
    * 已跟踪：本来就纳入版本控制管理的文件，上次快照中有它们的记录；
    * 未跟踪：不是已跟踪的文件；
5. 确定当前文件状态：`git status`；
6. 跟踪文件：`git add file`;如果是目录的话,就说明要递归跟踪所有该目录下的文件;
7. 如果`git add`后又做了修改，要重新运行`git add`暂存；
8. 忽略某些文件：
    * 创建一个名为`.gitignore`的文件；
    * 列出要忽略的文件格式，例如：
       <pre>
       .[oa]
       *~
       </pre>
    * `.gitignore` 的格式规范:
        * 所有空行或者以注释符号 # 开头的行都会被 Git 忽略;
        * 可以使用标准的 glob 模式(shell 正则表达式)匹配;
        * 匹配模式最后跟反斜杠( / )说明要忽略的是目录;
        * 要忽略指定模式以外的文件或目录,可以在模式前加上惊叹号( ! )取反;
9. 查看未暂存的文件与先前文件的差异： `git diff`;
10. 查看已经暂存起来的文件和上次提交时的快照之间的差异： `git diff --staged`;
11. 提交：
    * 每次提交前，使用`git status`查看是否已将全部想要的文件都暂存起来了；
    * `git commit`：启动文本编辑器输入本次提交的说明；
    * 跳过使用暂存区域，自动把所有已经跟踪过的文件暂存起来一并提交：`git commit -a`;
12. 移除文件：
    * `git rm file`;
    * 删除之前修改过并且已经放到暂存区域的文件：`git rm -f file`;
    * 仅从跟踪清单中删除：`git rm --cached file`;
13. 重命名：`git mv filefrom fileto`;用其他工具批处理改名的话,要记得在提交前删除老的文件名,再添加新的文件名;
14. 回顾提交历史：
    * `git log`;
    * `-p`选项展开显示每次提交的内容差异;
    * `-n`则仅显示最近的n次更新;
15. 提交错误或者有文件没有提交时：
    * 补上没提交文件的暂存操作；
    * `git commit --amend`;
16. 任何已经提交到 Git 的都可以被恢复；
17. 远程仓库origin 用的是 SSH URL 链接；
18. 查看有哪些远程仓库：`git remote -v`;
19. 从远程仓库抓取数据到本地：
    * `git fetch [remote-name]`;
    * 如果是克隆了一个仓库,上述命令会自动将远程仓库归于 origin 名下；
20. 查看某个远程仓库的详细信息: `git remote show [remote-name]`;
21. Git 使用的标签有两种类型：
    * 轻量级的(lightweight)：指向特定提交对象的引用；
    * 含附注的(annotated)：存储在仓库中的一个独立对象,它有自身的校验和信息,包含着标签的名字,电子邮件地址和日期,以及标签说明,标签本身也允许使用 GNU Privacy Guard (GPG) 来签署或验证；
    <pre>
    git tag -a v1.4 -m 'my version 1.4'
    </pre>
    * `-m`选项则指定了对应的标签说明,Git 会将此说明一同保存在标签对象中;
    * 列出已有的标签：`git tag`；
22. 将本地仓库中的数据推送到远程仓库: `git push [remote-name] [branch-name]`; 
    
    
