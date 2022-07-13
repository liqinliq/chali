## (一) git 仓库管理常用命令

仓库创建和入库操作

设置用户名密码
git config --global user.email "xxx@xxx.com"   // xxx@xxx.com 换成你的邮箱地址
git config --global user.name "xxxx"					 // xxxx换成你的用户名	
git init 初始化 git 仓库
添加文件到仓库
git add xxx // 添加xxx文件到仓库
git add . 把所有更改的文件添加到仓库
git status 查看状态(非必须)
git commit -m"xxx" 提交文件
撤销和删除操作

git checkout .放弃所有更改 实操: 修改test.js的内容,然后执行git checkout . 你会发现你所有的修改都没了
git clean -fd 删除新增文件但没对其执行过 git add 的文件
rm .git -rf 删除仓库(或者直接删除隐藏文件夹.git)

## (二) git 仓库中文件状态

仓库中的文件分为两大类:

未跟踪文件 - 未进行git add操作的文件
已跟踪文件 - 执行过git add操作的文件都是已跟踪的文件
vscode中文件末尾字母含义 U: 未跟踪的文件 A: 新增的文件 M: 被修改的文件 D: 被删除的文件 C: 有冲突的文件 更改和暂存中的更改

在[更改]区的文件表示文件被新增、删除、修改
对第1点中的文件执行git add , 这些文件就进入了[暂存的更改]区
对第2点中的文件执行 git commit, 这些文件就从[暂存的更改]区消失

## (三) 版本的前进和回滚

查看git log版本信信息


如果我们要回退到aaa这次操作提交上来，我们只需要将id复制一下，然后执行下面命令即可
git reset --hard e55640863f0eb141e0857761f0268c61121c07ac
回到上一个版本
git reset --hard HEAD^   // 回到上上个版本用 git reset --hard HEAD^^
版本回退之后，如果想再回到现在，你只需要记住你要回到的id即可使用同样的命令回到现在
如果不记得版本id，还可以使用git reflog来查看你提交的历史记录，从中找到版本的id，再进行reset操作
#

## (四) 本地仓库和远程仓库

在前面的一到四章节,我们所有的操作都是在本地进行的,本文主要讲解本地仓库与远程仓库的相关知识点

代码托管网站#

github 国际级别代码托管平台
码云 国产代码托管平台
coding 国产代码托管平台

### (1) 本地仓库和远程仓库常用命令

在码云网站注册一个账号, 然后新建一个仓库,复制仓库地址
git clone xxx(远程仓库地址) 把远程的仓库克隆到本地。例如:
git clone https://gitee.com/huruqing/gitdemo.git@git
如果仓库地址是 https 开头,则需要输入用户名密码
git remote add origin xxx 关联远程仓库,例如:
git remote add origin https://gitee.com/huruqing/gitdemo.git
git remote remove origin 断开与远程仓库的关联
git remote -v 查看关联的远程仓库
把本地仓库内容推送(同步)到远程仓库 git push origin xxx
git push origin master 推送到远程仓库的主干
git push origin dev 推送到远程仓库的 dev 分支
git push origin master -u // -u 下次推送不用加分支名称,直接使用 git push 即可
git push origin master -f // -f 强制推送,轻易不要使用
git pull拉取代码,把远程仓库的代码同步到本地仓库,如果本地有代码未提交,需要先提交然后推送才能拉取代码
#

### (2) 给码云配置公钥

请看第(五)点

### (3) 从0-1把一个项目放到码云

方式一:

git init
在码云上新建仓库得到一个仓库地址
关联仓库 : git remote add origin 仓库地址
git add .
git commit -m"init"
git push origin master -u (第2次提交使用git push)
添加文件, 重复4-5-6步
方式二:

在码云新建仓库, 复制仓库地址
执行 git clone 仓库地址, 在电脑里得到一个带有仓库信息的文件夹
把项目复制到第2步中的文件夹, 执行方式一中的4-5-6步即可

### (五) 给码云配置公钥

每次提交代码到码云的时候，都需要输入账户密码，真的很不方便，好在码云给我们提供了解决方案，只需要创建秘钥对，在码云上添加公钥就可以了，把私钥保存在本地即可，以下就是添加公钥的步骤。

打开 git bash
输入 ssh-keygen -t rsa -C "你的邮箱地址" 三次回车之后就可以生成密钥对
输入 cat ~/.ssh/id_rsa.pub 查看你的 public key（公钥），结果如下：


把途中从 ssh-ras（包含）到最后面的邮箱地址（包含）复制一下。
打开码云 -> 设置 -> SSH 公钥，就出现了下面的画面，把我们刚才复制的内容贴到提示区，最后点击左下角的确定即可。

### (六) .gitignore 忽略文件

有时候,有些文件或文件夹并不需要都推送到远程仓库,这时候,我们可以把它加入到忽略文件列表.具体做法:

在项目根目录添加.gitignore 文件
打开.gitignore 文件,添加你要忽略推送的文件,下面是一份忽略清单
.DS_Store 
node_modules 

### (七) 冲突处理

由于多人同时进行开发，有时候会同时修改一个文件，或者多分支开发，合并的时候就很容易引发冲突，下面是一个制造冲突和解决冲突的例子。

制造冲突#

同学 A 新建码云仓库,同时添加同学 B 为开发者(其实一个人也可以制造冲突的)
同学 A 新建文件 main.js 并提交推送到远程仓库,同学 B 把仓库同步到本地,这时两位同学都有一个 main.js 的空文件
同学 A 在 main.js 的第一行添加"我是同学 A",然后添加,提交并推送到远程仓库
同学 B 在 main.js 的第一行添加"我是同学 B",
然后执行以下命令
git add .
git commit -m"修改main.js"
git push origin master
出现以下提示


意思是被拒绝了,要先执行 git pull 命令

执行git pull命令,同学 B 的界面上出现了以下情况


 因为两位同学同时修改了同一行代码,所有 git 不知如何取舍(如果同学 a 修改了第一行,同学 b 修改了第二行,那么 git 会智能的合并),只好把合并代码这个事情交给开发者去处理,
上图中<<<<<<< HEAD 到========的代码是 B 同学的代码,
======到>>>>>>> a248f68a5fcbcbe4cc887bee3dfc3cfd1cf7147b 的代码是同学 a 的代码,括号的 Incoming Change 的意思是从外面来的修改,a248f68a5fcbcbe4cc887bee3dfc3cfd1cf7147b 是仓库是冲突的版本号,你可以通过 git log 看到详细的信息.
你可以根据具体情况去合并代码,取 a 的代码或者取 b 的代码,或者 a 取一点,b 取一点,具体情况具体分析
当同学 A 和同学 B 都修改了同一个地方的代码,同学 A 推送了代码,同学 B 执行了git add .命令,但没有执行git commit命令,就会出去下面的界面: 意思是要你先git commit,然后再git pull
合并工具#

使用 vscode 进行合并
beyond compare
其他的合并工具

### (八) 分支操作

git checkout -b dev     // 创建并切换到dev分支
git checkout master // 切换到主干分支
git branch        // 查看分支
git branch -a // 查看所有分支
git fetch -a // 拉取所有分支, 拉取之后使用git branch -a才能看到别人新建的远程分支
git push origin dev // 推送dev分支代码到远程仓库的dev分支
git pull origin dev:dev // 拉取远程dev分支
git merge dev -m"xxx" // 合并dev分支到主干分支(当前分支必须是master分支)
git merge master -m"xxx" // 合并master分支到dev分支(当前分支是dev分支)
#
​

### (九) 为什么有时候git pull(git push) 无法更新代码

1.提示没权限, 如下图:#



 原因:

可能你真的没有权限
你的项目没有关联远程仓库
没有网络或者网络卡
gitee网站的问题
2.出现以下提示:#



 原因: 在你提交之前, 已经有人先于你提交了, 你要先执行git pull把对方的代码更新下来, 再去执行git push。 ​

3.无法git pull#

本地仓库修改了代码, 需要先commit后才能执行git pull 操作

### (十) 可视化工具

vscode集成了git,很多操作可以通过鼠标操作
github desktop, 下载地址 GitHub Desktop | Simple collaboration from your desktop
sourcetree
小乌龟git 下载地址 Git for Windows

### (十一) 码云添加开发者

登录码云
打开项目
点击管理
点击开发者
点击添加仓库成员(5个)
