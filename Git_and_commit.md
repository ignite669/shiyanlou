### Git 与GitHub的来历

Git 是Linux之父Linus用c语言写的开源的版本控制系统

同名网站GitHub是用Ruby编写的，这是一个基于Git的免费代码托管网站(有付费服务，但是被微软收购后，私人仓库也是免费使用的)



```shell
#GitBash中编写如下代码
git --version


```





### Git仓库的三大区域



注意所有Git命令都以**git**开头

#### 创建仓库

![1563275760389](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563275760389.png)

![1563275841178](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563275841178.png)

#### 克隆仓库到本地仓库

```
git clone git@github.com:ignite669/shiyanlou.git
```

![1563268099696](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563268099696.png)

进入仓库主目录中有个.git隐藏目录

里面包含了仓库的全部信息，删掉这个目录，仓库就变成普通目录了。进入当仓库目录中

```
lscd shiyanlou
```

进入到仓库目录中，命令行前缀发生了变化 出现了master,它就是当前的分支名

当我们在GitHub上创建一个仓库时，同时发生了仓库的默认主机名origin,主机就是指代仓库本身，主机名就等于仓库地址，git并创建了默认分支master.

克隆一个GitHub仓库(远程仓库)到本地，本地仓库则会自动关联到这个远程仓库，

```
#查看本地仓库所关联的远程仓库信息
git remote -v
```

![1563274880832](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563274880832.png)

克隆远程仓库到本地时，还可以使用-o选项修改主机名，在地址后面加上一个字段作为本地仓库的主目录名

```
git clone -o originnn https://github.com/ignite669/shiyanlou.git haha
```

![1563275502498](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563275502498.png)

![1563275647176](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563275647176.png)

另一个在Git教程中常见的命令git init 它会把当前所在目录变成一个本地仓库，因为有GitHub的存在，这个命令在我们的生产生活中用到的次数应该时零，除非你想费时费力自己搭建服务器

#### 完整的修改，提交，推送

```
cd shiyanlou
git status #查看整个仓库的状态

```

![1563276414231](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563291505376.png)

![1563276582784](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563276582784.png)

ls 表示列出当前目录的文件 

```
echo "文件内容" > 文件名 #原文件会被覆盖
echo “文件内容" >> 文件名 #在文件末尾追加内容
```

如上图所示，新建文件后，命令行前缀红色master后面出现*星号 这表示工作区或者暂存区发生变化，对文件进行操作都会出现这个星号，可使用 **git status** 命令可查看详情

#### 添加修改到暂存区

```
#git add [文件名]
git add one.txt
git status
```

![1563276833073](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563276833073.png)

如果对多个文件或者目录进行增删改，可以使用git add . 命令全部添加到暂存区

当我们修改了工作，git add 命令式将这些修改添加到暂存区，暂存区记录的只是修改。

#### 撤销暂存区的修改

```
#git reset --[文件名]或者git rm -- cached[文件名]
#注意--后面至少有一个空格
git reset -- one.txt
git reset -- #把暂存区的全部修改撤销 ，回到工作区
```

![1563277465048](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563277465048.png)

撤销暂存区的修改之后，就回到了工作区

查看工作区被修改详情,版本区中存在的文件才是被跟踪文件

```
git diff
按Q可以退出工作区修改详情页
ls
```

![1563279418527](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563279418527.png)

```
git diff #此时位于工作区 所以查看工作区修改内容
注意 echo 修改文件时 注意""必须都是英文，有一个中文就不行 不会正常修改成功
```

![1563279477329](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563281296112.png)

```
按q可以退出此页面
```

将工作区的修改添加到暂存区,并使用 git diff --cached 查看暂存区全部修改git 

```
#添加全部修改到暂存区
git add 
q
```

![1563281419071](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563281419071.png)

![1563280262776](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563281447925.png)



**把暂存区的修改提交到版本区，生成一个新的版本**

```
git commit
```

![1563280441857](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563284331308.png)

#### 配置个人信息

```
git config --global user.email "ignite678@126.com"
git config --global user.name "ignite669"
#注意该空格隔开的一定要空格隔开，不然会配置失败

#查看配置信息
git config -l 
```

![1563285451962](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563285451962.png)



```
cat -n ~/.gitconfig
```

![1563285536243](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563285536243.png)

可以手动修改上面的配置文件

#### 提交暂存区的修改

```
#-m选项来提交该提交的备注
git commit -m "提交的备注"
```

![1563285821993](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563285821993.png)

提交后，残存区的修改被清空，执行 git log 查看提交记录

![1563285871995](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563285871995.png)

commit 后面的十六进制序列号就是提交版本号，每个提交都有自己单独的版本号，这很重要，就像公民身份证号一样

提交信息 提交版本是按时间倒序排列的，你可能查看时间正序排列的信息，可以使用

```
git log --reverse
```

```
#用来查看全部分支信息
git branch -avv 
```

![1563286226276](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563286226276.png)

**第一行** 开头的星号表示当前所在分支，绿色的master是分支名，绿色是表示当前所在分支

第二项 是版本号 

第三项中挂号里面蓝色的字 表示此分支跟踪的远程分支的名字 

创建master分支 并自动跟踪远程同名分支

：冒号后面黑色文章表示本地分支领先其跟踪的远程分支一个提交

最好一项是提交时填项的备注信息



第二行，Git指针信息，它指向远程仓库的master分支，这行信息咱不重要

第三行 远程分支信息 

执行commit命令 并不推荐-a 它的作用是将未添加到暂存区的修改，也就是工作区的修改也一并提交，但是会忽略未被跟踪的文件



#### 推送到远程仓库

![1563293336781](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563293336781.png)

在GitHub中查看

![1563293359064](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563293359064.png)

![1563293399164](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563293399164.png)

### Git分支操作

#### 一 添加SSH关联授权

创建SSH公密钥之后，生产GitHub账户对于当前系统中的Git授权。

这样每次提交就不用手动输入用户名和密码

```
#终端执行
ssh-keygen 
#按几次回车生成公秘钥，公秘钥存放在家目录下的隐藏目录.ssh中的两个文件中

```

![1563293835451](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563293835451.png)

将~/.ssh/id_rsa.pub文件中的公钥内容复制出来，

![1563293930839](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563293930839.png)

**重要的一点：只有使用这种 git 开头的地址克隆仓库，SSH 关联才会起作用。**

使用 SSH 的好处主要有两点：

- 免密码推送，执行 `git push`时不再需要输入用户名和密码了；
- 提高数据传输速度。它不是必须的，比如在实验楼的课程中挑战环境是不可保存的，一次性的，这种环境就没有必要创建 SSH 了，因为相较好处来说，还是太麻烦了。

#### 版本回退

**撤销提交**

```
#撤销最近一次提交
git reset --soft HEAD^#--soft 表示软退回，--hard 硬退回
#HEAD^表示撤销一次提交
#HEAD^^表示撤销两次提交
#HEAD~n 表示撤销n次


```



#### ![1563299662131](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563299662131.png)处理commit时间线分叉

![1563299426974](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563299426974.png)

```
git status #查看仓库状态
git branch -avv #分支状态

```

![1563299505223](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563299505223.png)

**提交时间线分叉：**

本地仓库的master分支与远程仓库的origin/master 分支在提交版本上有了冲突

因为

刚才的提交操作并不是基于远程仓库origin/master分支的最新提交版本，而是撤回了一个版本。

这种情况下也是可以将本地master分支推送到远程仓库的，需要加一个选项-f  他是--force的简写 ，就是强制推送

```
#强制推送 
git push -f
```

![1563299981483](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563300060036.png)

git branch -avv 查看本地master与远程master的版本号一致 前四位都是a308 刷新GitHub页面 结果如预期

![1563300239021](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563300239021.png)

#### 本地仓库commit变化记录

执行git reflog查看本地记录所有分支的每一次版本变化

```
#查看本地仓库记录的版本变化
git reflog
```

![1563300423141](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563300423141.png)

如何回退呢？

```
git reset --hard[版本号]
git reset --hard HEAD@{2}#回到当前分支最近两次提交版本变话前
```

![1563300576038](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563300736512.png)

### Git分支操作

#### 一 添加SSH关联授权

终端执行 ssh-keygen  命令 按几次回车生成公私钥  公私钥存在目录下的隐藏目录  .ssh中的两个文件中

![1563511384332](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563511384332.png)

将~/.ssh/id_rsa.pub文件中的公钥内容复制出来，实验环境中可以使用右侧工具栏中的剪切版复制

![1563511653445](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563511653445.png)

注意使用cat哦

```
rm -rf shiyanlou #删除原仓库
#克隆仓库是需要确认连接的，输入yes即可
```

![1563512011312](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563512011312.png)

只有使用git开头的地址克隆仓库，SSH关联才会起作用

使用SSH的好处主要有两点：

免密码推送。执行git push 时 不再需要输入用户名和密码了

提高数据传输速度。

#### 二 为Git命令设置别名

```
#为命令设置别名 ，如果原命令中不是一个单词，需要加引号英文
git config --global alias.别名 原命令

```

![1563512909880](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563512909880.png)

别名是自定义的 设置后 原命令和别名具有同等作用

```
#查看配置文件 使用的别名
git config -l
```

![1563513136595](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563513136595.png)

#### 三 分支管理

****

#### git fetch 刷新本地分支信息

#将远程仓库的分支信息拉取到本地仓库

#仅仅是更新了本地的远程分支信息  

执行bit branch -avv 命令时查看到的remotes开头的行的分支信息

```
#执行fetch命令刷新保存在本地仓库的远程分支信息
git fetch
```



![1563517137821](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563517137821.png)

```

```

![1563517206797](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563517206797.png)

```
#使本地master分支的提交版本为最新
#拉取远程仓库的数据到本地
git pull 

#由于执行过git fetch 也可以执行
git rebase origin/master #实现‘使本地分master分支基于远程仓库master分支“

```

![1563518368358](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563518368358.png)

可以看到远程仓库 master分支 本地仓库origin/master分支，本地仓库master分支已经一致。

#### 创建新的本地分支

**why:分支在本地项目开发中作用重大，多人协作 不可或缺**

列如 在项目中，需要创建新的分支来存放测试版的代码

再例如 实验课的课程团队在维护课程仓库时，每个人都有各自得分支，在自己得分支上修改，然后向master分支提PR( pull request ),最后从master分支推送到线上



首先克隆远程仓库到本地，进入仓库主目录 ，执行git br 查看分支信息

![1563519151977](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563519151977.png)

```
#创建分支
git branch [分支名]

```

![git 1563519329804](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563519329804.png)



```
#创建新分支后并未切换到新分支，还是在master分支上
git checkout [分支名]#切换分支

#给常用命令checkout设置别名
git config --global alias.ch checkout
#查看配置别名信息
cat -n ~/.gitconfig
或者是 
git config -l
```

![1563519793219](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563519793219.png)

![1563519922171](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563519922171.png)

```
#创建新分支并且切换到新分支
git checkout -b [分支名]
```

![1563520087247](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563520087247.png)

如图所示，前两行是新建的本地分支信息

他们的版本号与主分支master一致

这是因为在哪个分支上创建新分支，新分支的提交记录就与哪个分支一致

新分支并无跟踪任何远程分支，所有没有master分支中的中括号和括号内的蓝色远程分支名

![1563520785205](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563520785205.png)

```
#在当前分支dev1上开发一个新功能，需要增加一个文件new_func1 生成一个新的提交
echo '新功能测试' > new_func1

```

![1563521379531](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563521379531.png)



#### 将新分支中的提交推送至远程仓库

```
#将本地分支推送到远程仓库的分支中，如果远程分支不存在，会自动创建
git push [主机名] [本地分支名]：[远程分支名]
#如果冒号前后的分支名是相同的，可以省略
git push [主机名] [本地分支名]


```

![1563522272932](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563522272932.png)

![1563522456384](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563522456384.png)

可以看到  远程分支origin/dev1 的信息已经在本地存在，且与本地同名分支一致。

![1563522662102](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563522662102.png)

#### 本地分支跟踪远程分支

当我们再次在dev1 分支上修改并提交，推送到远程仓库是还是要输入上面的长长的命令，好不方便

```
#将本地分支与远程分支关联 或者说本地分支跟踪远程分支  
git branch -u [主机名/远程分支名] [本地分支名]
#如果设置当前所在分支跟踪远程分支 最后一个参数本地分支名可以省略不写
git branch -u [主机名/远程分支名]
```

![1563523193736](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563523193736.png)

-u选项是 --set-upstream 的缩写  

#本地分支跟踪远程非同名分支 ,可以的 纯属自找麻烦的需求

##### #撤销分支对远程分支的跟踪

```
#撤销该分支跟踪远程分支
git branch --unset-upstream [分支名]
#如果撤销当前所在的分支的跟踪
分支名可以省略不写
```

![1563523810145](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563523810145.png)

前面的操作是先将本地分支推送到远程仓库，使远程仓库创建新分支，然后再执行命令使本地分支跟踪远程分支。

#### 推送本地分支自动跟踪远程分支

```
#推送的时候加上 --set-upstream 或其简写-u
git push -u origin dev
```

![1563524786129](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563524786129.png)

#### 删除远程分支

```
#删除远程分支
git push [主机名][空格]：[远程分支名]
#删除多个远程分支
git push [分支名][空格]:[远程分支名] ：[远程分支名] ：[远程分支名]
#此命令的原理 是将空分支推送到远程分支，结果自然就是远程分支被删除
#另一个删除远程分支的命令
git push [主机名] --delete [远程分支名]
#删除远程分支可以在任意本地分支中执行

```

![1563525962458](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563525962458.png)

在本地仓库中已经没有远程分支的dev dev1的分支信息

![1563526024982](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563526024982.png)

查看GitHub仓库页面

只剩一个master分支 ，。操作成功

#### 本地分支的更名与删除

```
#给本地分支改名
git branch -m [原分支名] [新分支名]#若修改当前所在分支的名字，原分支名可以省略不写
#删除本地分支
git branch -D [分支名] [分支名]’
```

![1563531122362](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563531122362.png)

当前所在分支不能被删除，需要切换到master

![1563532452940](C:\Users\ASUS\AppData\Roaming\Typora\typora-user-images\1563532452940.png)



#### 待更新 多人协作GitHub部分

#### 多人协作Git