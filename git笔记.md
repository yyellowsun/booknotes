### git初始化：git init 

git remote add origin git@github.com:yyellowsun/test.git

origin是对后面git@github.com:yyellowsun/xxx.git的名字,把本地库与远程库建立连接

git push -u origin master

将本地master分支推送到origin,-u的含义是什么？



### 把远程库的内容拉到本地

git pull -r remote local

git pull所做的东西：1、git fetch remote-repo

​									  2、git merger remote/master local

-r指令表示使用rebase



### 使用git rebase合并commit

使用git reset --hard commitID 来回退到指定版本

--hard:表示把改动全部丢弃

--soft:在本地保留改动，丢掉commit

### 使用git remote add upstream xxx
git remote add upstream  为本地fork的库添加远程库
git remote remove upstream
git fetch upstream 从远程库捕获



Git:一个文件存储系统。工具包的设计：可以看做plumbing和porcelain两种工具。

Git 对象：

Blobs:用hash算出来的40个字符的十六进制串。只存储文件内容，不存储文件名，文件模式。意味着：对于不同名的相同文件，拥有相同的blobs，在仓库转移的时候只会转移一次文件内容，但是checkout的时候会把两个文件都checkout出来。

Tree:存储着tree和blobs，以及他们的名字和模式。用一个文本文件存储tree，blobs的hash值，名字，类型，模式。

Commit:存储Tree的历史记录的存储系统。指向一个Tree记录作者，提交者，message,以及之前的commit。一般情况，一个commit指向一个father commit.但是如果合并两个branch，则会得到指向两个branch的两个commit。

Tag:相当于给commit起一个别名。里面有commit对象的hash值，类型，tag，tagger,message.

Git 数据模型：有向非循环图。

​    Git里面存储不可变对象：object,和可变对象：reference.(ex:branch,remotes),

​    每次一个新的提交，从最底层改的blobs开始，找blobs的父结点，一直找到commit，然后用一个新的commit,指向旧的commit，以前没变的blobs和tree就继续保留，增添新的改变了的blobs和tree。

​    如何遍历呢。从./git/refs里面找到commit，然后从顶层开始往下遍历。

 

​    

 

Branch:一个branch就是存储在.git/refs/head文件夹里面的一个文件,存储着这个分支最近一次commit的哈希值。所以创建一个分支就是往一个文件夹里面存储一个文件，往一个文件里面写哈希值。

​    切换branch:

​    Switching to that branch simply means having Git make your working directory look like the tree that SHA-1 points to and updating the HEAD file so each commit from that point on moves that branch pointer forward (in other words, it changes the 40 characters in .git/ refs/heads/[current_branch_name] be the SHA-1 of your last commit).

 

Remote:针对clone下来的仓库，会自动默认添加一个orgin/master的远程分支，这样clone下来会有两个reference，一个是master是本地的分支，指向本地最近的一次commit，另一个是orgin/master指向你克隆的那个库的那个时候的master分支。

 

Rebasing:并不是将我的commit，和别人的commit给合并，而是，将我做的修改作为补丁文件与别人的commit了，得到一个新的commit，和merge非常不一样！！！原因是merge的指针会指向两个，但是rebase只有一个。相当于你和别人同步做一个工作，别人提交了，你也改完了，然后你给merge了，这么做了多次，历史记录会变得杂乱。所以你rebase，相当于，别人远程交了，你给改了别人的代码，得到新的commit.