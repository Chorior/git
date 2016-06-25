#git学习总结
---
>作者：彭侦  
>链接：<https://github.com/Chorior/git/blob/master/Personal%20Summary%20of%20git.md> 

Distributed Version Control System,简称DVCS,中文翻译为分布式版本管理系统,在管理代码方面简直就是神一般的存在,下面是我个人在两周之内学习git pro的总结,其中有一些参考了其它文章。

##本文结构
* [git安装](#git安装)
* [创建一个远程代码库](#创建一个远程代码库)
* [git配置](#git配置)
* [创建本地仓库](#创建本地仓库)
* [加载文件](#加载文件)
* [移动文件](#移动文件)
* [提交文件](#提交文件)
* [建立分支](#建立分支)
* [合并分支](#合并分支)
* [衍合分支](#衍合分支)
* [删除分支](#删除分支)
* [添加远程仓库](#添加远程仓库)
* [推送数据到远程仓库](#推送数据到远程仓库)
* [删除远程仓库](#删除远程仓库)

<h2 id="git安装">git安装</h2>
1. linux
    * Fedora: `sudo yum install git-core`
    * Debian: `sudo apt-get install git-core`
2. Windows
    * 从<http://code.google.com/p/msysgit>下载安装文件.exe,点击安装即可
    * 若需要翻墙,这里提供lantern的下载地址:<https://github.com/getlantern/lantern>

<h2 id="创建一个远程代码库">创建一个远程代码库</h2>
1. 上<http://github.com>注册一个账号,并新建一个代码库；
2. 这里有一篇文科妹子写的github教程: <https://gold.xitu.io/entry/56e638591ea49300550885cc>

<h2 id="git配置">git配置</h2>
1. 配置个人用户名和电子邮件
    * `git config --global user.name pengzhen`
    * `git config --global user.email pengzhen@example.com`
2. 配置文本编辑器
    * git在需要你输入一些信息的时候,会调用一个文本编译器
    * 如果不设置的话,可能默认调用nano编辑器,一般使用vi或者vim会比较方便
    * 配置编辑器为vi: `git config --global core.editor vi`
3. 配置好之后查看配置信息: `git config -l`
4. 如果忘记配置的话,git不会让你提交任何东西

<h2 id="创建本地仓库">创建本地仓库</h2>
有两种创建本地仓库的方法  

1. 在现存目录下,通过导入所有文件来创建新的git仓库  
    * 去往所要进行git管理的项目目录
    * 执行`git init`,执行结束之后会在当前目录下生成一个.git隐藏目录,所有git需要的数据和资源都存放在该目录下   
2. 从已有git仓库克隆一个新的镜像仓库  
    * 如果你有一个远程代码库<github.com/Chorior/git>
    * 执行`git clone git://github.com/Chorior/git.git mygit`会在当前目录下创建一个名为mygit的目录,其内含一个.git的目录,并包含了所有远程仓库的数据
    * 你也可以使用ssh或者http(s)代替git

<h2 id="加载文件">加载文件</h2>
1. 首先检查当前文件的状态: `git status`
2. 查看未跟踪文件列表与已跟踪列表
3. 移除已跟踪文件并删除工作目录下该文件: `git rm file_tracked`
4. 移除已跟踪文件但不删除工作目录下该文件: `git rm --cached file_tracked`
5. 取消暂存已跟踪的文件: `git reset HEAD file_tracked`
6. 跟踪文件: `git add file_untracked`
7. 如果跟踪文件之后修改了该文件,使用`git diff`查看当前目录下文件与已跟踪文件的差异
8. 如果想取消对某个文件的修改,回到上次提交的文件状态: `git checkout -- file_modified`
8. 如果项目里一些文件经常变动,比如编译之后生成的.o,.a文件,或者记录项目结果的xml文件,这些都不需要跟踪，这时可以在项目根目录下新建一个.gitignore文件,里面写好不需要跟踪的文件的格式,配置语法如下:
    * 以井号“#”开头代表注释
    * 以斜杠“/”结尾表示目录
    * 以星号“*”通配多个字符
    * 以问号“?”通配单个字符
    * 以方括号“[]”包含单个字符的匹配列表
    * 以叹号“!”表示不忽略(跟踪)匹配到的文件或目录

<h2 id="移动文件">移动文件</h2>
1. git不记录文件的移动，但它会推知文件的更名操作
2. 使用`git mv file_from file_to`

<h2 id="提交文件">提交文件</h2>
1. 提交已跟踪文件: `git commit`,运行之后会弹出设置好的编辑器以便输入此次提交的说明,为空是不能提交的
2. 查看提交历史: `git log`,显示内容为:
    * 每次提交第一行为对应提交的SHA-1校验和
    * 每次提交第二行为作者姓名和邮件地址
    * 每次提交第三行为提交时间
    * 每次提交第四行缩进一个段落显示提交说明
3. 如果提交结束之后发现自己手残有几个文件忘记加了,或者有文件修改忘记更新了,又或者提交信息写错了，首先加载忘记提交的文件或者修改过但没提交的文件，运行 `git commit --amend`会撤销上次的提交并重新开始新的提交

<h2 id="建立分支">建立分支</h2>
1. 如果你想建立一个项目的镜像,使用分支操作,只需要一秒时间，不管项目有多大，都能成功镜像出来
2. 建立当前项目的一个分支: `git branch new_branch`
3. 查看分支列表: `git branch`
4. 切换到一个分支: `git checkout new_branch`
5. 新建并切换到该分支: `git checkout -b new_branch`
6. 执行`git log`查看提交历史后想回到某一个历史状态: `git checkout commit_SHA-1`
7. 新建一个历史分支: `git checkout -b new_branch commit_SHA-1`

<h2 id="合并分支">合并分支</h2>
1. 如果你想合并某一个分支到另外一个分支
2. 在源分支上加载已更新文件并提交；
3. 切换到目标分支
4. 执行`git merge src_branch`将源分支合并到目标分支

<h2 id="衍合分支">衍合分支</h2>
1. 衍合即将一个分支的更新操作在另一个分支中重做一遍
2. 切换到要衍合的分支
3. 执行`git rebase [des_branch]`

<h2 id="删除分支">删除分支</h2>
1. 切换到主分支: `git checkout master`
2. 删除不要的分支: `git branch -d other_branch`
3. 强制删除不要的分支: `git branch -D other_branch`

<h2 id="添加远程仓库">添加远程仓库</h2>
1. 使用`git remote add [shortname] [url]`,如`git remote add origin git@github.com:Chorior/git.git`
2. 抓取远程仓库有的但本地主干分支没有的数据: `git fetch [shortname]`
3. 抓取远程仓库数据并自动合并到某一分支: `git pull [shortname] [branch_name]`
4. 修改远程仓库的简短名称: `git remote rename [short_name] [new_short_name]`

<h2 id="推送数据到远程仓库">推送数据到远程仓库</h2>
`git push [remote_name] [branch_name]`

<h2 id="删除远程仓库">删除远程仓库</h2>
`git remote rm [short_name]`
