# CedarGuo.github.io

1、content目录里放的是你写的markdown文章，layouts目录里放的是网站的模板文件，static目录里放的是一些图片、css、js等资源，
theme是主题格式，public存放所有编译后的静态页面，也是推送到github的文件夹。

博客日志，最好将md文件放在site/content/post目录里。

2、本地启动Hugo参考：https://www.gohugo.org/

hugo server --theme=hyde --buildDrafts

3、部署到github pages：

上传博客到post路径之后，需要在站点根目录执行hugo命令生成最终页面：

在站点根目录执行：hugo --theme=hyde --baseUrl="http://cedarguo.github.io/" ，注：这里要用github pages提供的地址，通常大写换成小写字母。

baseUrl为浏览器可部署之后访问的路径，参考“仓库》settings》pages”，theme为自己的主题名。（这些都可以在site/config.toml中设置）

命令执行后，所有静态页面都会生成到 site/public 目录。
只需将pubilc目录里所有文件 push 到刚创建的Repository的 master 分支即可。

git操作：
git init , 在本地创建Git仓库（site/public目录下）

git remote add origin https://github.com/CedarGuo/CedarGuo.github.io.git(git远程仓库地址) , 是指本地仓库和远程仓库建立连接。

git add -A , git add命令可将该文件添加到暂存区

git commit -m "first commit"，提交暂存区文件到本地仓库中，提交信息必填

git push -u origin master 初次关联远程仓库以后使用，关联本地仓库到远程仓库的master 分支。以后直接git push即可。

以上操作创建的是https连接，每次push需要输入github的token，实现免密登录（ssh连接）：

首先需要创建ssh密钥：

本地生成sshkey：ssh-keygen -t ed25519 -C "your_email@example.com"（git bash）

在github上添加sshkey :  https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account

测试ssh 连接：ssh -T git@github.com（https://docs.github.com/cn/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection）

然后可以删除本地仓库与远程仓库的原有http连接，创建ssh连接：（下面命令在site/public目录下执行，是一个git仓库）

git remote rm origin

git remote add origin git@github.com:CedarGuo/CedarGuo.github.io.git（git远程仓库地址）

git add -A

git commit -m "ssh 连接测试"

git push -u origin master，之后git push即可，push比较慢，可能会超时，多试几次。

注：如果提示连接失败，可能是网络原因，重试ssh -T git@github.com 或者 ssh -T -p 443 git@ssh.github.com即可。

注：如果连接超时，可以在host文件中手动添加dns映射：
140.82.113.4 github.com
140.82.113.4 www.github.com

注：如果远程repo和本地repo冲突，通常由于在github远程仓库上更改了文件，本地未更改，导致了远程和本地的冲突。
先把远程repo pull到本地，然后再push。
git pull origin master
git push origin master

注：如果是本地init仓库，直接push到远程仓库时，会提示仓库冲突，是因为刚建的远程仓库里有readme文件。这时候需要先git pull origin master，同上。

但是此时还会报错：拒绝合并不相关的历史fatal: refusing to merge unrelated histories，因为本地仓库和远程仓库实际上是独立的两个库。
执行： git pull origin master --allow-unrelated-histories 即可。

4、外网访问
http://CedarGuo.github.io/


5、配置文件config.toml：

baseURL = 'http://example.org/' 改为自己的网站地址

theme = "hugo-academic-group" 改为自己theme文件夹下的主题

