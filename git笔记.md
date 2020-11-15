git初始化：git init 

git remote add origin git@github.com:yyellowsun/test.git

origin是对后面git@github.com:yyellowsun/xxx.git的名字,把本地库与远程库建立连接

git push -u origin master

将本地master分支推送到origin,-u的含义是什么？



把远程库的内容拉到本地

git pull -r remote local

git pull所做的东西：1、git fetch remote-repo

​									  2、git merger remote/master local

-r指令表示使用rebase



使用git rebase合并commit

使用git reset --hard commitID 来回退到指定版本

--hard:表示把改动全部丢弃

--soft:在本地保留改动，丢掉commit

