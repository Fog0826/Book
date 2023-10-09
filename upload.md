# 记录我第一次从本地上传大于25MB的文件的过程

1. cd upload 
  
  进入本地名为upload的文件夹，提前将要上传的大文件放入该文件夹下
2. git init 
  
  创建本地仓库环境
3. git lfs install 
  
  安装大文件上传应用
4. git lfs track * 
  
  追踪要上传的大文件，*表示路径下的所有文件
5. git add .test 
  
  添加先上传的属性文件(要先上传属性文件，不然有可能失败)
6. git commit -m "test" 
  
  添加属性文件上传的说明
7. git remote add origin https://github.com/Fog0826/Book.git
  
  建立本地和Github仓库的链接
8. git push origin master 
  
  上传属性文件
9. git add * 
  
  添加要上传的大文件，*表示路径下的所有文件
10. git commit -m "Git LFS commit" 
  
  添加大文件上传的说明
11. git push origin master 
  
  上传大文件  

在第一次执行第9步的时候会出现
```
fatal: unable to access 'https://github.com/Fog0826/Book.git/': Failed to connect to github.com port 443 after 75048 ms: Couldn't connect to server
```
我查阅了gpt：这个错误消息 "Failed to connect to github.com port 443" 表示你的 Git 客户端无法连接到 GitHub 服务器的 443 端口，这通常是由于网络问题、防火墙、代理或其他网络配置问题引起的。

通过查阅“stackoverflow”论坛，我尝试了前几个方法，但是都没有得到正确的解决，最后通过一个大哥的回复
```
git config --global http.proxy XXX.XXX.XXX.XXX:ZZ
```
其中 XXX.XXX.XXX.XXX 是代理服务器地址，ZZ 是代理服务器的端口号,通过自己的代理查看，就我而言，无需指定任何用户名或密码。输入终端的命令：
```
git config --global http.proxy 127.0.0.1:7890
```
接下来我就正确的避开防火墙访问到GitHub
但是在继续执行第9步的时候，我又遇到了以下问题

```
fog@FogMacBook-Pro upload % git push origin master
Username for 'https://github.com': Fog0826
Password for 'https://Fog0826@github.com': 
remote: Support for password authentication was removed on August 13, 2021.
remote: Please see https://docs.github.com/en/get-started/getting-started-with-git/about-remote-repositories#cloning-with-https-urls for information on currently recommended modes of authentication.
fatal: Authentication failed for 'https://github.com/Fog0826/Book.git/'
```
这个错误表示对密码身份验证的支持已于 2021 年 8 月 13 日删除，所以这时候我们不能通过账号密码顺利去访问github仓库，我在“stackoverflow”论坛上找到了一个适用于macos系统的解决办法
  
首先，在github上创建个人访问令牌
  Settings → Developer Settings → Personal Access Token → Generate New Token (Give your password) → Fillup the form → click Generate token → Copy the generated Token, it will be something like `ghp_sFhFsSHhTzMDreGRLjmks4Tzuzgthdvfsrta`
  上述是创建个人令牌的方式，我在创建过程中选择的是第二个经典的选项，还有一个beta的版本我没有试过，同时注意在创建中需要勾选上`repo`选项，否则token是没有权限访问GitHub仓库的，并且token只会展示一次，之后不再展示，需要记录好自己的token
  
其次，第二步我按照教程走并没有在keychain access中找到github的语句，可能是我通过谷歌浏览器进行访问，cookie数据并没有存在keychain access中，所以我更换了一种方式

```
git remote set-url origin https://<githubtoken>@github.com/<username>/<repositoryname>.git
```

在终端中运行了这个命令，将<githubtoken>，<username>，<repositoryname>（仓库名称）进行替换成自己的数据，然后就

```
fog@FogMacBook-Pro upload % git push origin master
Uploading LFS objects: 100% (1/1), 54 MB | 1.3 MB/s, done.                                          
Counting objects: 9, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (8/8), done.
Writing objects: 100% (9/9), 922 bytes | 922.00 KiB/s, done.
Total 9 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
remote: 
```

大功告成，在开始的一些步骤也出现了一些小问题，但是我觉得不如最后两个问题来的有难度，就不一一记录了（其实是我也忘记了，大体记得安装了homebrew然后搜了一下七七八八的就解决了）