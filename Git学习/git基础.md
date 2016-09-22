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

### 查看配置信息

```
$ git config --list
$ git config user.name
```

## 获取帮助

了解Git的各式工具该怎么用的三种方法

```
$ git help <verb>
$ git <verb> --help
$ man git-<verb>

//例如，学习config命令
$ git help config
```

## 取得项目的Git仓库

有两种取得 Git 项目仓库的方法。第一种是在现存的目录下，通过导入所有文件来创建新的 Git 仓库。第二种是从已有的 Git 仓库克隆出一个新的镜像仓库来。

### 在工作目录中初始化新仓库

```
$ git init
```

初始化后，在当前目录下会出现一个名为 .git 的目录，所有 Git 需要的数据和资源都存放在这个目录中。不过目前，仅仅是按照既有的结构框架初始化好了里边所有的文件和目录，但我们还没有开始跟踪管理项目中的任何一个文件。

### 从现有仓库克隆

如果希望在克隆的时候，自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字

    // 这会在当前目录下创建一个名为`grit`的目录，其中包含一个 `.git` 的目录，用于保存下载下来的所有版本记录，然后从中取出最新版本的文件拷贝。
    $ git clone git://github.com/schacon/grit.git

    // 如果希望在克隆的时候，自己定义要新建的项目目录名称，可以在上面的命令末尾指定新的名字 
    $ git clone git://github.com/schacon/grit.git mygrit

Git 支持许多数据传输协议。之前的例子使用的是 `git://` 协议，不过你也可以用 `http(s)://` 或者 `user@server:/path.git` 表示的 SSH 传输协议。

## 记录每次更新到仓库

### 检查当前文件状态

使用`git status`命令

工作目录相当干净

```
$ git status
On branch master
nothing to commit, working directory clean
```

有文件未跟踪

```
$ vim README
$ git status
On branch master
Untracked files:
 (use "git add <file>..." to include in what will be committed)

 README

nothing added to commit but untracked files present (use "git add" to track)
```

文件以暂存

```
$ git status
On branch master
Changes to be committed:
 (use "git reset HEAD <file>..." to unstage)

 new file: README
```

已跟踪文件发生变化

```
$ git status
On branch master
Changes to be committed:
 (use "git reset HEAD <file>..." to unstage)

 new file: README

Changes not staged for commit:
 (use "git add <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)

 modified: benchmarks.rb
```

以暂存文件再次修改，此时提交会提交修改之前的版本

```
$ vim benchmarks.rb
$ git status
On branch master
Changes to be committed:
 (use "git reset HEAD <file>..." to unstage)

 new file: README
 modified: benchmarks.rb

Changes not staged for commit:
 (use "git add <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)

 modified: benchmarks.rb
```

###跟踪新文件
使用`git add`命令
这是个多功能命令，根据目标文件的状态不同，此命令的效果也不同：
- 可以用它开始跟踪新文件
- 或者把已跟踪的文件放到暂存区
- 还能用于合并时把有冲突的文件标记为已解决状态等

