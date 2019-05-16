---
layout: post
title: "继续上一篇未完成的工作时碰到的新问题"
date: 2019-05-17
categoties: original
---

决定开一个新的txt记录碰到的新问题- -我已经不想再来回修改要上传的那一个了= =<br>
1）push到git的指令 git push origin master报错显示'origin' does not appear to be a git repository<br>
重新输入一次：git remote add origin git@github.com:yourusername/test.git然后再输入：git push -u origin master 就可以提交了<br>
由此出现的新问题，提交的时候出现了Warning: Permanently added the RSA host key for IP address '13.229.188.59' to the list of known hosts.<br>
显示为电脑公钥未添加至git所以无法识别，首先查看本地是否有SSH密钥：cd ~/.ssh<br>
如果没有的话首先生成密钥：ssh-keygen -t rsa -C "youremail"<br>
由此出现的新问题- -failed to push some refs to'git@github.com:xxx/xxx.git'<br>
原因： GitHub远程仓库中的README.md文件不在本地仓库中。<br> 
解决方案：$ git pull --rebase origin master  $ git push -u origin master<br>
由此带来的新问题= =我已经要昏迷了<br>
Pulling is not possible because you have unmerged files.在pull的时候出现的问题，问题来自于本地文件冲突，需要reset，具体方法为git reset --hard FETCH_HEAD<br>
这之后在更新本地差异文件时发生问题， It seems that there is already a rebase-apply directory,根据提示git rebase --skip尝试第一次解决问题，目前看来问题成功解决，成功将本地文件push到远端仓库啦^_^这之中的一些尝试因为急于睡觉以及种种原因，解决的很懵懂，希望下次再次碰到这些问题的时候我还能想起这篇文章orz。<br>
= =打扰了并没有push上去，显示的依然是第一次push的内容，看看问题出在哪里先<br>
错误提示为Everything up-to-date，问题出在没有git add或者没有git commit -m “提交信息”，- -我明明已经做过了啊，总之先重来一圈试试看<br>
错误提示为没东西可提交- -nothing to commit, working tree clean，目前发现我是真的没东西可提交（（（（（总之先改点东西重新提交一下试试- -<br>
尝试用git pull --rebase提交差异文件报错， Your index contains uncommitted changes.原因是如果有未提交的更改是不能git pull的，首先要执行git stash暂存正在进行的工作，然后在pull，最后git stash pop从git栈中读取最后一次保存的内容<br>
太乱套了决定从clone开始重来一遍- -<br>
上传虽然成功了但是没能成功显示界面，寻找解决办法中<br>
无论如何都只能显示最远古版本的界面，目前决定先清空仓库里的文件让他变成一个新仓库然后再push一次= =不知道为什么会发生这样的问题，希望以后遇到的时候能明白吧<br>
然后发现了分支的这个问题，现在能显示出来的界面都是gh-pages分支下的，暂时不明白为什么会发生这种问题，首先尝试一下把gh-pages分支删除<br>
git push origin --delete 分支名<br>
删除之后界面直接404了- -决定重新翻阅一下最开始的教程，思路是想找到为什么只有在那个分支下才能显示网页，可能是有些设置上的问题我没有处理。<br>
找不出问题，打算先把gh-pages分支添加回来再重新上传jekyll试试。<br>
