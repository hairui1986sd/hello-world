# GIT和GitHub教程

### 1. 下载安装Git

访问官网：https://git-scm.com/，下载并安装；

初次安装git需要配置用户名和邮箱，否则git会提示：please tell me who you are.

你需要运行命令来配置你的用户名和邮箱：

$ git config --global user.name "hairui1986sd"

$ git config --global user.email "hairui1986sd@163.com"

查看自己的用户名和邮箱地址：

　　$ git config user.name

　　$ git config user.email

**注意：（引号内请输入你自己设置的名字，和你自己的邮箱）**　　

用户名和邮箱地址相当于你的身份标识，是本地Git客户端的一个变量，不会随着Git库而改变。每次commit都会用用户名和邮箱纪录，并不是github用户名和邮箱。github的contributions跟你的邮箱是有关联的。

git支持https和git两种传输协议，github分享链接时会有两种协议可选：

git使用https协议，每次pull, push都会提示要输入密码；使用git协议，然后使用ssh密钥，这样免去每次都输密码的麻烦。

**初次使用git的用户要使用git协议大概需要三个步骤：**

**一、生成密钥对**

大多数 Git 服务器都会选择使用 SSH 公钥来进行授权。系统中的每个用户都必须提供一个公钥用于授权，没有的话就要生成一个。生成公钥的过程在所有操作系统上都差不多。首先你要确认一下本机是否已经有一个公钥。

SSH 公钥默认储存在账户的主目录下的 ~/.ssh 目录。进去看看：

$ cd ~/.ssh

$ ls

authorized_keys2  id_dsa       known_hosts config            id_dsa.pub

看一下有没有id_rsa和id_rsa.pub(或者是id_dsa和id_dsa.pub之类成对的文件)，有 .pub 后缀的文件就是公钥，另一个文件则是密钥。

假如没有这些文件，甚至连 .ssh 目录都没有，可以用 ssh-keygen 来创建。该程序在 Linux/Mac 系统上由 SSH 包提供，而在 Windows 上则包含在 MSysGit 包里：

https://github.com/hairui1986sd/hello-world/blob/master/images/1555770900538.png

到此为止，你本地的密钥对就生成了。

**二、设置远程仓库（本文以github为例）上的公钥**

 1、查看你生成的公钥：

$ cat ~/.ssh/id_rsa.pub

ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC5AroS1uz+ICUydDK1D8RUAqcsnFJq5jxPJ2VVQLXVwQKrGbw8UOkPMsANJVoUK7d/OmZsxqx/TtthyJjfZOGUzatPzkPwzI5Myys4bss4CiASmRIcPYlw0ZXSdG53HTgGFVMahFbKPtRtc7jiW8cNXmBKq8FvN9/XWHYThkoTPcAVN4d2WbOP1NEUZTPJCrHcUwpMe5HJ8wuQiheaG5YzolmWoTp/p2bEOPYIVu5llU7Y42UbTStxEsYID2Wrs2DVsrBILrYKwd6vhTi61RH2tHwW1OOr+2k+vOchXLH/vY/AEDKYwWZin/t7xCYtHVdOpUwGT66Qg/WERXAkNX83 hairui1986sd@163.com

2、登陆你的github帐户。点击你的头像，然后Settings -> 左栏点击 SSH and GPG keys -> 点击 New SSH key

3、然后你复制上面的公钥内容，粘贴进“Key”文本域内。 title域，自己随便起个名字。

4、点击 Add key。

完成以后，验证下这个key是不是正常工作：

$ ssh -T git@github.com

Attempts to ssh to github

如果，看到：

Hi xxx! You've successfully authenticated, but GitHub does not # provide shell access.

恭喜你，你的设置已经成功了。

**三、把git的 remote url 修改为git协议**（以上两个步骤初次设置过以后，以后使用都不需要再次设置，此步骤视以后项目的remote url而定，如果以后其他项目的协议为https则需要此步骤）

使用命令 git remote -v 查看你当前的 remote url

$ git remote -v

origin https://github.com/someaccount/someproject.git (fetch)origin https://github.com/someaccount/someproject.git (push)

如果是以上的结果那么说明此项目是使用https协议进行访问的（如果地址是git开头则表示是git协议）

你可以登陆你的github，就像本文开头的图例，你在上面可以看到你的ssh协议相应的url，类似：



![img](https:////upload-images.jianshu.io/upload_images/4690961-f9c0a393ed42fcb4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/411/format/webp)



复制此ssh链接，然后使用命令 git remote set-url 来调整你的url。

git remoteset-url origin git@github.com:someaccount/someproject.git

然后你可以再用命令 git remote -v 查看一下，url是否已经变成了ssh地址。

然后你就可以愉快的使用git fetch, git pull , git push，再也不用输入烦人的密码了。

### 2. 注册并使用GitHub

访问GitHub官网注册账号：https://github.com/；

使用刚注册的账号登录；

#### 2.1 创建新仓库

1. 在右上角，在您的头像或identicon旁边，单击 然后选择**New repository**。
2. 命名您的存储库`hello-world`。
3. 写一个简短的描述。
4. 选择**使用自述文件初始化此存储库**。

![1555764154069](C:\Users\hairui\AppData\Roaming\Typora\typora-user-images\1555764154069.png)

最下面方框中勾选的‘ Initialize this repository with a README`：初始化本库，可选择可不选择，这里分为两种演示方式，先演示不选择的。

##### 不选择（不初始化仓库）

`这种方式，是先初始化本地git，再把git提交成远程分支的`

![1555771552525](C:\Users\hairui\AppData\Roaming\Typora\typora-user-images\1555771552525.png)

新建文件夹tes-git。其实这就到了命令初始化git了，如果你是window用户的话，自行创建一个文件夹（test-git），然后shift+右键，选中"在这里打开命令行"，然后跳过linux建目录的过程。

如果你是linux的话，要么自行定义文件夹，要么按照流程跟我走，我们打开命令行，linux如下：

```
cd ~
mkdir test-git（文件夹名）
cd test-git/ 
```

首先到达home目录，创建一个文件夹名叫test-git，再进入到文件夹里面。

###### 命令创建git分支

> 提示：这里window用户请使用git带的git base

在创建库时（如上图），他会给以提示，如上面的图片，然后你照着页面上的命令一行一行的往下输：

```
echo "# -git-" >> README.md （说明：echo "# 这里是你要创建的git项目的名字"）
```

输入完成打开文件则有一个叫README.md的文件，如图：

![1555772194036](C:\Users\hairui\AppData\Roaming\Typora\typora-user-images\1555772194036.png)

再输入

```
git init
```

初始化一个git本地仓库，初始完git后，如果你是window用户，你会在目录里看到一个`.git`文件夹，这就说明本地初始化git成功了，然后输入

```
git add README.md
```

给git本地仓库添加文件README.md（本地仓库工作区--》暂存区）。

添加完以后，需要进行托付（本地仓库暂存区--》仓库区），并写明托付原因：

```
git commit -m "first commit"
```

其中-m后面的"first commit"就是你要写的托付原因，当然也是支持汉语的。

接下来就是，添加远程仓库（本地创建的仓库与远程仓库关联起来）：(注意后面的链接是你创建github项目时，自动生成的)

```
git remote add origin https://github.com/hairui1986sd/test.git
```

添加完远程仓库分支后，接下来就是提交这个分支了（本地仓库--》远程仓库）：

```
git push -u origin master
```

这里的master指的是主分支名，如果是其他分支，则填写相应的分支名。提交的时候会要求你输入你的帐号和密码，如果没有要求也无关紧要，输入完成以后到我们的项目里看，它就创建成功了，如图：

![1555773223170](C:\Users\hairui\AppData\Roaming\Typora\typora-user-images\1555773223170.png)

##### 选择（选中`Initialize this repository with a README(初始化本库)`）

**先创建远程分支，再下拉到本地的。**

他会直接先把远程库创建好，如图：![1555773530965](C:\Users\hairui\AppData\Roaming\Typora\typora-user-images\1555773530965.png)

我们则需要把这个远程库拉到本地就可以了。点击绿色按钮clone or download，复制里面的链接，我们再次打开命令行，linux如下：(window请打开`Git bBash Here`)

```
cd /d/Developer/Workspaces/git
```

然后使用clone命令，从远程库拉一个分支，在git的文件夹下生成hello-world文件夹：

```
git clone https://github.com/hairui1986sd/hello-world.git
```

然后添加文件（加入所有修改）：

```
cd hello-world
git add .
```

给git添加文件之后就和上面的步骤相同了，添加完以后，就该写托付，并写明托付原因：

```
git commit -a
```

这里使用-a来，当然上面的`git commit -m "first commit"`也是可以的。

最后`git push`，进行推送提交。

链接：https://www.jianshu.com/p/deb5eddbffb8

来源：简书

简书著作权归作者所有，任何形式的转载都请联系作者获得授权并注明出处。





附

#### 1. SSH Key

**SSH 密钥对** 最直观的作用：**让你方便的登录到 SSH 服务器，而无需输入密码**。由于你无需发送你的密码到网络中，SSH 密钥对被认为是更加安全的方式。

原因是：SSH利用SSH Key来进行前面提到的基于密钥的安全验证。

**使用SSH key的步骤：**

- 在客户端生成SSH key（密钥对：公钥和私钥）
- 在服务端的配置文件中加入你的公钥。（比如我们需要再GitHub中粘贴你的公钥）

#### 2. Git 常用命令

如果你只是修改文件则直接：`git commit -a`，然后自动进入vim编辑器，你在英文输入法下按`i`键，然后在最上面一栏输入提交的内容(随便说说你都干了什么)，然后`esc`，英文输入法下：`shift+：`输入`wq`(w保存，q退出)，就可以了。

如果你有添加新文件，则在`git commit -a`之前添加一句`git add -A`就可以了，意思是添加所有的文件(包含你新添加的文件)到git版本控制器。

提交了项目，下来就是把信息推送到`git`分支上了，直接输入：`git push` 就可以了。

如果有其他人在分支上修改了东西，你需要把最新的git信息拉到你的本地git，这时你也只需要在你的项目文件里打开命令行，直接输入`git pull`就可以了。

提交成功后，可以用git log查看历史提交记录。每个记录都会有提交id，作者和提交日期。

你可以用git branch查看当前有哪些分支，当然，因为我们没有创建任何分支，目前只会有一个master分支。可以使用git checkout -b feature创建一个名为feature的分支。

#### 3. 项目的下载，查看和修改
第一步. 从GitHub上下载我们的项目代码。

1. 以Hello-World项目为例，点击绿色按钮Clone or download，然后在弹出窗口中点击剪切板图标，复制仓库的URL。

2. 在git bash中输入git clone https://github.com/hairui1986sd/hello-world.git，下载项目源码。

第二步. 查看版本历史
1. cd到项目文件夹下，使用git log能看到我们的历史提交记录。

2. 要回到某一历史版本，可以使用git checkout commitId，看完后要回到最新代码，使用git checkout master。

第三步. 本地修改代码
你可以在我们的代码基线上任意修改，但为了下载新代码时不出现冲突，请遵循以下步骤：

1. 下载新代码：git pull。

2. 从master出捡出一个新的分支：git checkout -b feature。feature是分支名称，你可以随意取名，但请用英文。

3. 在feature分支上随意修改，改完后你可以提交你的修改：git commit -m "some message"。

4. 此时要同步代码，请先切回主分支：git checkout master，然后更新git pull。

5. 如果想删除自己建立的分支，使用git branch -D feature，注意执行此命令后分支被强制删除，无法恢复。

