# Version Control
---
1. 版本控制：
    * 版本控制是一种记录若干文件内容变化，以便将来    查阅特定版本修订情况的系统；
    * CVCS：Centralized Version Control Systems；
        * 只要整个项目的历史记录被保存在单一位置,就有丢失所有历史更新信息的风险;
    * DVCS：Distributed Version Control System；
        * 客户端并不只提取最新版本的文件快照,而是把原始的代码仓库完整地镜像下来；
        * 任何一处协同工作用的服务器发生故障,事后都可以用任何一个镜像出来的本地仓库恢复；
2. Git 和其他版本控制系统的主要差别：
    * Git 只关心文件数据的整体是否发生变化；
    * 而大多数其他系统则只关心文件内容的具体差异；
    * 每次提交更新时,Git会纵览一遍所有文件的指纹信息并对文件作一快照,然后保存一个指向这次快
照的索引;
    * 若文件没有变化,Git 不会再次保存,而只对上次保存的快照作一连接;
3. Git优点：
    * 在 Git 中的绝大多数操作都只需要访问本地文件和资源,不用连网;            
    * 在保存到 Git 之前,所有数据都要进行内容的校验和(checksum)计算,并将此结果作为数据的唯一标识
和索引；
    * Git 使用 SHA-1 算法计算数据的校验和,通过对文件的内容或目录的结构计算出一个 SHA-1 哈希值,作为指纹字符串，所有保存在 Git 数据库中的东西都是用此哈希值来作索引的,而不是靠文件名；
    * 常用的 Git 操作大多仅仅是把数据添加到数据库，不用担心丢失数据的问题；
4. 任何一个文件,在 Git 内都只有三种状态：
    * 已提交（committed）：该文件已经被安全地保存在本地数据库中；
    * 已修改（modified）：修改了某个文件，但还没有提交保存；
    * 已暂存（staged）：把已修改的文件放在下次提交时要保存的清单中；
5. Git 管理项目时,文件流转的三个工作区域：
    * 本地数据目录：保存元数据和对象数据库的地方；
    * 工作目录：从项目中取出某个版本的所有文件和目录,用以开始后续工作的目录；
    * 暂存区域：简单的文件,一般都放在 git 目录中；
6. 基本Git工作流程：
    * 在工作目录中修改某些文件；
    * 对这些修改了的文件作快照,并保存到暂存区域；
    * 提交更新,将保存在暂存区域的文件快照转储到 git 目录中；
7. 安装Git:
    * ubuntu：`sudo apt-get install git-core`
    * Fedora：`sudo yum install git-core`
    * Mac：`sudo port install git-core +svn +doc +bash_completion +gitweb`
    * Windows：<http://code.google.com/p/msysgit>
8. Git工作环境变量存放在三个不同的地方：
    * `/etc/gitconfig` 文件:系统中对所有用户都普遍适用的配置。若使用 `git config`时用 `--system` 选项,读写的就是这个文件；
    * `~/.gitconfig`文件:用户目录下的配置文件只适用于该用户。若使用 `git config`时用 `--global` 选项,读写的就是这个文件；
    * 工作目录中的`.git/config`：这里的配置仅仅针对当前项目有效;每一个级别的配置都会覆盖上层的相同配置,所以`.git/config`里的配置会覆盖`/etc/gitconfig`中的同名变量；
9. 配置：
    * 第一个要配置的是你个人的用户名称和电子邮件地址：
        * 每次 Git 提交时都会引用这两条信息，说明是谁提交了更新；
        * 如果用了`--global`选项,那么更改的配置文件就是位于你用户主目录下的那个,以后你所有的项目都会默认使用这里配置的用户信息;如果要在某个特定的项目中使用其他名字或者电邮,只要去掉--global选项重新配置即可,新的设定保存在当前项目的`.git/config`文件里。
        <pre>
        git config --global user.name "John Doe"
        git config --global user.email johndoe@example.com
        cat ~/.gitconfig
        </pre>
    * 第二个要配置的是默认使用的文本编辑器：
        * 默认会使用操作系统指定的默认编辑器,一般可能会是 Vi 或者 Vim；
        * 更换为Emacs：`git config --global core.editor emacs`
    * 选择配置差异分析工具：
        * `git config --global merge.tool vimdiff`   
    * 查看配置信息：
        * `git config --list`;
        * 直接查阅某个环境变量的设定: `git config user.name`;
