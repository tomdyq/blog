# vscode连接git问题解决

vscode中对git进行了集成，很多操作只需点击就能操作，无需写一些git指令。

1.  安装Git管理工具，可上官网安装，安装路径[https://git-scm.com/](https://git-scm.com/)，安装路径默认C:\Program Files\Git，可自行修改，这里我是安装在D:\Program Files\Git。
2.  安装完Git之后，如图配置好环境变量path路径的信息，一般会自动配置成功，配置完成后电脑就可以使用Git了。
3.  要想在VS Code里面使用Git需要在编辑器内配置git.path
配置步骤：在编辑器的文件->首选项->设置->搜索git.path->点击编辑->找到你的电脑git的安装目录，找到里面的bin文件夹，里面的git.exe文件把该文件的完整路径复制下来。比如"git.path": "D:/Program Files/Git/bin/git.exe",
4. VSCode中Git的使用以及Github的免密上传
> * 首先设置一下全局变量，以下命令直接在git-bash终端上输入即可，成功之后会在你的电脑用户跟目录下生成一个 .gitconfig的配置文件，里面包含着你的用户名及密码
>> Git 全局设置:
>> (1) git config --global user.name "用户名" 
>> (2) git config --global user.email "用户邮箱"

> * 接下来就是上传代码到github上,在上传之前先在github上创建库。
>> (1) 创建完成后进入vscode打开终端进入要上传的项目的根目录之后执行git初始化仓库命令`git init`,
>> (2) 执行添加文件目录到git仓库命令 `git add .` （. 小数点是添加当前目录下的所有文件 也可以只添加制定文件或者文件夹）
>> (3) 执行上传到git仓库命令`git commit -m "可写注释内容"`
>> (4) 执行git仓库与github仓库的连接命令`git remote add origin https://github.com/你的github的用户名/test.git`（这里是你创建的仓库名字加上 .git）
>> (5) 执行推送到分支(master)的命令`git push -u origin master`（分支名字master为主分支）
>> (6) 在你第一次使用时点击推送或者执行上条push的命令时会弹出github的登入框，输入用户名密码（在vscode中每次push都要输入用户名密码，这里可以执行git命令让git软件记住密码）如下:`git config --global credential.helper store`,后面就不需要密码了。
>> (7) 执行到这里就可以到github上面查看你刚才新建的github仓库了，点开里面就是你的项目了，success

5. vscode因为集成了git所以vscode的有些按钮可替代上面输入的git命令。<font color='red'>加号->对勾->pull</font>

## 问题

1. <b>问题</b>:git push到GitHub的时候遇到! [rejected] master -> master (non-fast-forward)的问题
<b>解决办法</b>：
> (1) git pull origin master --allow-unrelated-histories //把远程仓库和本地同步，消除差异
> (2) 重新add和commit相应文件
> (3) git push origin master
> (4) 此时就能够上传成功了
