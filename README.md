<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<title>git操作</title>
	<style type="text/css">
		div>h1{text-align: center;}
		div>h1>a{text-decoration: none;}
		h4{color:red;}
		div.all>p{margin-left: 30px;}
	</style>
</head>
<body>
<div>
	<h1>
		<a href='http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013758392816224cafd33c44b4451887cc941e6716805c000'>git操作</a>
	</h1>
</div>
<h3>git常见错误</h3>
<div class="all">
	<h4>一、$ git remote add origin git@github.com:xxx(帐号)/gitdemo(项目名).git,提示出错信息：fatal: remote origin already exists.</h4>
<p>
  解决办法如下：<br/>
   		1、先输入$ git remote rm origin<br/>
   		2、再输入$ git remote add origin git@github.com:djqiang/gitdemo.git<br/>
   		3、如果输入$ git remote rm origin 还是报错error: Could not remove config section 'remote.origin'.
         我们需要修改gitconfig文件的内容：找到github的安装路径，找到一个名为gitconfig的文件，打开它把里面的[remote "origin"]那一行删掉就好了！
</p>


<h4>
	二、如果输入:$ ssh -T git@github.com出现错误提示：Permission denied (publickey).因为新生成的key不能加入ssh就会导致连接不上github。
</h4>
<p>
	解决办法如下：<br/>
      1、先输入：  $ ssh-agent  再输入：  $ ssh-add ~/.ssh/id_key<br/>
      2、如果输入:ssh-add ~/.ssh/id_key 命令后出现报错：Could not open a connection to your authentication agent.<br/>
        解决方法：key用Git Gui的ssh工具生成,这样生成的时候key就直接保存在ssh中了,不需要再ssh-add命令加入,其它的user,token等配置都用命令行来做.<br/>
      3、最好检查一下在你复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的
</p>
<h4>
	三、如果输入:$ git push origin master 提示出错信息：error:failed to push some refs to .......
</h4>
<p>
	解决办法如下：<br/>
      1、先输入:  $ git pull origin master //先把远程服务器github上面的文件拉下来   再输入:  $ git push origin master<br/>
      2、如果出现报错 fatal: Couldn't find remote ref master或者fatal: 'origin' does not appear to be a git repository
         以及fatal: Could not read from remote repository.则需要重新输入:$ git remote add origin git@github.com:djqiang/gitdemo.git
</p>
<h4>
	四、使用git在本地创建一个项目的过程:
</h4>
	<p>$ makdir ~/hello-world    //创建一个项目hello-world</p>
     <p>$ cd ~/hello-world       //打开这个项目</p>
     <p>$ git init             //初始化</p>
     <p>$ touch README</p>
     <p>$ git add README        //更新README文件</p>
     <p>$ git commit -m 'first commit'   //提交更新，并注释信息“first commit”</p>
     <p>$ git remote add origin git@github.com:defnngj/hello-world.git //连接远程github项目 </p> 
     <p>$ git push -u origin master   //将本地项目更新到github项目上去</p>

  	 <p>配置相关信息:</p>
            <p>4.1　当你安装Git后首先要做的事情是设置你的用户名称和e-mail地址。这是非常重要的，因为每次Git提交都会使用该信息。它被永远的嵌入到了你的提交中：</p>
			<p>$ git config --global user.name "John Doe"</p>
			<p>$ git config --global user.email johndoe@example.com</p>
           <p>4.2  你的编辑器(Your Editor)</p>
			现在，你的标识已经设置，你可以配置你的缺省文本编辑器，Git在需要你输入一些消息时会使用该文本编辑器。缺省情况下，Git使用你的系统的缺省编辑器，这通常可能是vi 或者 vim。如果你想使用一个不同的文本编辑器，例如Emacs，你可以做如下操作：</p>
			<p>$ git config --global core.editor emacs</p>
 
            <p>4.3 检查你的设置(Checking Your Settings)</p>
			<p>如果你想检查你的设置，你可以使用 git config --list 命令来列出Git可以在该处找到的所有的设置:</p>
			<p>$ git config --list</p>
            <p>你也可以查看Git认为的一个特定的关键字目前的值，使用如下命令 git config {key}:
                            $ git config user.name</p>
 
            <p>4.4 获取帮助(Getting help):</p>
            <p>如果当你在使用Git时需要帮助，有三种方法可以获得任何git命令的手册页(manpage)</p><p>帮助信息:</p>
            <p> $ git help</p>
            <p> $ git --help</p>
            <p> $ man git-</p>
            <p>例如，你可以运行如下命令获取对config命令的手册页帮助:</p>
            <p>  $ git help config</p>
<h4>五、gitconfig配置文件:Git有一个工具被称为git config，它允许你获得和设置配置变量；这些变量可以控制Git的外观和操作的各个方面。这些变量可以被存储在三个不同的位置：</h4>
  
            <p> 1./etc/gitconfig 文件：包含了适用于系统所有用户和所有库的值。如果你传递参数选项’--system’ 给 git config，它将明确的读和写这个文件。</p>
            <p>  2.~/.gitconfig 文件 ：具体到你的用户。你可以通过传递--global 选项使Git 读或写这个特定的文件。</p>
             <p> 3.位于git目录的config文件 (也就是 .git/config) ：无论你当前在用的库是什么，特定指向该单一的库。每个级别重写前一个级别的值。因此，在.git/config中的值覆盖了在/etc/gitconfig中的同一个值。</p>

       <p>  在Windows系统中，Git在$HOME目录中查找.gitconfig文件（对大多数人来说，位于C:\Documents and Settings\$USER下）。它也会查找/etc/gitconfig，尽管它是相对于Msys 根目录的。这可能是你在Windows中运行安装程序时决定安装Git的任何地方。</p> 

  <h4>六、push到github时，每次都要输入用户名和密码的问题"</h4>
  <p>在github.com上 建立了一个小项目，可是在每次push的时候，都要输入用户名和密码，很是麻烦</p>
   <p>原因是使用了https方式 push</p>
    <p>在termail里边 输入  git remote -v</p>
    <p>可以看到形如一下的返回结果</p>
    <p>origin https://github.com/dengVictor/learngit.git (fetch)</p>
    <p> origin https://github.com/dengVictor/learngit.git (push)</p>

    <p>下面把它换成ssh方式的。</p>
    <p>1. git remote rm origin</p>
    <p>2. git remote add origin git@github.com/dengVictor/learngit.git</p>
    <p>3. git push origin</p>

    <h4>七、常用命令:</h4>
      <p>假如你现在新创建了一个项目，想把它提交到github上面？</p>
      <p>假设你创建好了一个项目，并切换到项目的根目录下面：</p>
       <p> $ git status查看当前项目下所有文的状态，如果第一次，你会发现都红颜色的，因为它还没有交给git/github管理。</p>
       <p>$ git add .   //（.）点表示当前目录下的所有内容，交给git管理，也就是提交到了git的本地仓库。</p> 
        <p>Ps:git的强大之处就是有一个本地仓库的概念，在没有网络的情况下可以先将更新的内容提交到本地仓库。</p>
        <p> $ git commit –m”discription ”  //对你更新或修改了哪些内容做一个描述。</p>
        <p>$ git remote add origin git@github.com:xiahouzuoxin/zx-libsvm.git</p>
        <p>// 如果你是第一次提交项目，这一句非常重要，这是你本地的当前的项目与远程的哪个仓库建立连接。</p>
        <p> Ps: origin可以改为别人的名字，但是在你下一次push（提交）时，也要用你修改之后的名字。</p>
        <p> $ git remote -v  //查看你当前项目远程连接的是哪个仓库地址。</p>
        <p> $ git push -u origin master  //将本地的项目提交到远程仓库中。</p>
    <hr>
    <p>假如，你回到了家，想把公司提交的项目克隆到本地？</p>
    <p> 如果你是第一次想把github上面的项目克隆到本地或者要克隆别人的项目到地。</p>
    <p>$ git clone git@github.com:xiahouzuoxin/zx-libsvm.git</p>
    <p>//在git下面切换到想存放此项目的文件目录下，运行这条命令就可以将项目克隆下来。</p>
    <p>假如本地已经存在了这个项目，而仓库中又有一新的更新，如何把更的合并到本地的项目中？</p>
    <p>$ git fetch origin    //取得远程更新，这里可以看做是准备要取了</p>
    <p> $ git merge origin/master  //把更新的内容合并到本地分支/master</p>

   <hr>
   <p>项目中删除了一些文件，如何提交？</p>
   <p>假如远程仓库中已经存了aaa这个文件，我fetch了下来，并删除了aaa这个文件，想再push上到远程仓库中，并使远程仓库中的项目被新的修改覆盖（也就是远程仓库中的aaa也被删除）</p>
   <p>$ git status   //可以看到我们删除的哪些文件</p>
   <p>$ git add .   //删除之后的文件提交git管理。</p>
   <p>$ git rm   src/com/hzh/hibernate/dao/aaa.java  </p>  
	<p>//移除我们删除的那个文件，不然git不允许我们往远程仓库提交。</p>
   <p>Ps: 如果你想删除的是某个目录（java包），这里想移除整个目录的内容。</p>
   <p>$ git rm  src/com/hzh/hibernate/bbb/ -r   // -r 会把bbb/目录下的所有内容一次性移动。</p>

   <hr>
   <p>远程创建了一个新仓库，本地创建了一个新项目，如何使新的项目与仓库对应起来？</p> 
   <p> 其实，这个也很简单，只是我当时对那些命令不太理解，所以比较模糊，不知如何对应。</p> 
   <p>  $ git remote add origin git@github.com:xiahouzuoxin/zx-libsvm.git</p> 
   <p> //还是这个命令，在你push项目之前加上这一句就OK了。</p> 
   <p> git@github.com:xiahouzuoxin/zx-libsvm.git </p> 
   <p>就是你常见的新仓库的地址啊。git切换到新项目下，在push之前，加上这一句，我们创建的新仓库就与新项目建立了连接。</p> 
</div>



</body>
</html>
