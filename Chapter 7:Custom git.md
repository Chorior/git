# Custom Git
---
1. 使用 `core.editor` 改变默认编辑器: `git config --global core.editor emacs`;
2. 将特定的策略运用在提交信息上: `git config --global commit.template $HOME/.gitmessage.txt`;
3. 格式化与空白：
    * Windows使用回车和换行两个字符来结束一行；
    * Mac和Linux只使用换行一个字符；
    * 提交时自动地把行结束符CRLF转换成LF,而在签出代码时把LF转换成CRLF: `git config --global core.autocrlf true`;
    * 提交时把CRLF转换成LF,签出时不转换: `git config --global core.autocrlf input`;
    * 设置 false 取消此功能: `git config --global core.autocrlf false`;