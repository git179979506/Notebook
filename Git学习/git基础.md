## 初次运行Git前的配置

* git config --system ：系统中对所有用户都普遍适用的配置
* git config --global ：用户目录下的配置文件只适用于该用户
* git config ：当前项目的git目录的配置文件（也就是工作目录中的`.git/config`文件）
* 每一级别的配置都会覆盖上层相同的配置

### 用户信息

```
$ git config --global user.name "userName"
$ git config --global user.email "email"
```

### 文本编辑器

修改默认的编辑器（mac是vim？）

```
// 例如修改为Emacs
$ git config --global core.editor emacs
```

### 差异分析工具

在解决冲突时使用哪种差异分析工具。Git 可以理解 kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等合并工具的输出信息。

```
$ git config --global merge.tool vimdiff
```

###查看配置信息

```
$ git config --list
$ git config user.name
```

##获取帮助
了解Git的各式工具该怎么用的三种方法

```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>

//例如，学习config命令
$ git help config
```

##取得项目的Git仓库
有两种取得 Git 项目仓库的方法。第一种是在现存的目录下，通过导入所有文件来创建新的 Git 仓库。第二种是从已有的 Git 仓库克隆出一个新的镜像仓库来。

### 在工作目录中初始化新仓库

```
$ git init
```


