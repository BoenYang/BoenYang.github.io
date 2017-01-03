title: 开始使用Hexo
data: 2016-11-10 21:05:39
---
Hexo的确是一个很好的博客工具，比起Jekyll以及Octopress都简单方便很多，最值得一提的是没有采用Ruby之类的，而是采用的Nodejs，环境搭建起来就简单很多了。

在我花了很短的时间搭建了博客后，我突然发现Hexo在Hexo deploy之后并没有将写过的博客源文件上传到Github上，这意味了写的博客源文件没有保存，这对于以后的博客迁移带来了困难，比如你要换台电脑，就需要拷贝好source，theme以及等等一些配置文件，看起来好像很不方便的样子。

手动的像Jekyll一样建立一个分支把要保存的文件提交到Github的非master分支是一个不错的解决方案。但是对于如此，我确认为不完美！！做为一个懒惰的程序猿，这种事情应该交给程序去完成嘛。在查看了hexo-deployer-git插件的源代码后（位于node_modules\hexo-deployer-git\lib\deployer.js）中，我发现对它进行修改，增加提交源文件的功能就可以了嘛，于是开干。

修改后的代码就成了这样子了：

添加了gitBaseDir函数
```
  function git(){
    var len = arguments.length;
    var args = new Array(len);

    for (var i = 0; i < len; i++){
      args[i] = arguments[i];
    }

    return spawn('git', args, {
      cwd: deployDir,
      verbose: verbose
    });
  }
  
  function gitBaseDir(){
	var len = arguments.length;
    var args = new Array(len);

    for (var i = 0; i < len; i++){
      args[i] = arguments[i];
    }

    return spawn('git', args, {
      cwd: baseDir,
      verbose: verbose
    });
  }
```

添加了提交source等文件的操作
```
  function push(repo){
    return git('add', '-A').then(function(){
      return git('commit', '-m', message).catch(function(){
        // Do nothing. It's OK if nothing to commit.
      });
    }).then(function(){
      return git('push', '-u', repo.url, 'master:' + repo.branch, '--force');
    }).then(function(){
      return gitBaseDir('checkout','source');
	}).then(function(){
	  return gitBaseDir('add','-A').then(function(){
		return gitBaseDir('commit','-m',message).catch(function(){
			
		});
	  });
	}).then(function(){
		return gitBaseDir('push','-u',repo.url,'source:source','--force')
	});
  }
```

这样就大功告成了，以后只需要
```
hexo new
hexo generate
hexo deploy 
```

就可以把生成的静态站点和source等文件都保存到github上了，是不是很爽


在使用这段代码之前，应该先在source文件所在的文件夹执行以下命令，初始化仓库，添加服务器信息，新建source分支
```
git init 
git remote add origin git@github.com:your_name:your_repo.git
git add .
git commit -m ""
git checkout -b source
```

虽然实现了这个功能，但是我觉得代码还是很挫，毕竟推送的分支是直接在代码写死的，而且还要进行上面的操作，我更希望可以在_config.yml中添加一个分支配置选项，然后再hexo-deployer-git插件中实现自动初始化仓库，添加服务器信息，新建分支等功能。
