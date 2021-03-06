# Git on the server
---
1. Git四种主要传输数据的协议：
    * 本地传输：将硬盘上的另一个目录作为远程仓库；
    * SSH协议：
        * 唯一一个同时便于读和写操作的网络协议；
        * 通过 SSH 进行访问是安全的——所有数据传输都是加密和授权的；
        * SSH 很高效,会在传输之前尽可能的压缩数据；
        * 不能通过它实现仓库的匿名访问;
    * Git协议：
        * 现存最快的传输协议；
        * 监听一个提供类似于 SSH 服务的特定端口(9418),而无需任何授权；
        * 最难架设的协议；
        * 要求防火墙开放 9418端口，大型企业级防火墙通常会封锁这个少见的端口；
    * HTTP协议：
        * 易于架设；
        * 企业级防火墙通常都允许其端口的通信；
        * 没有按需供应的能力——传输过程中没有服务端的动态计算；
2. 在服务器架设Git:
    * 把现存仓库导出新的纯仓库（不包含当前工作目录的仓库）：`git clone --bare my_project my_project.git`；
    * 将纯目录转移到服务器：`scp -r my_project.git user@git.example.com:/opt/git`；
3. 使用git push前：
    * 需要设置`push.default`；
    * 设置`push.default`为`matching`: 
        * `git config --global push.default matching`;
        * git 将推送和远程同名的所有本地分支；
    * 设置`push.default`为'simple'（老版本Git为'current'）：
        * `git config --global push.default simple`；
        * 只推送当前分支到远程关联的同名分支；
4. 使用git push推送当前分支；        