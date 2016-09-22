## 初次运行Git前的配置

* `git config --system` ：系统中对所有用户都普遍适用的配置
* `git config --global` ：用户目录下的配置文件只适用于该用户
* `git config` ：当前项目的git目录的配置文件（也就是工作目录中的`.git/config`文件）
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

### 跟踪新文件\/暂存已修改文件

使用`git add`命令
这是个多功能命令，根据目标文件的状态不同，此命令的效果也不同：

* 可以用它开始跟踪新文件
* 或者把已跟踪的文件放到暂存区
* 还能用于合并时把有冲突的文件标记为已解决状态等

### 忽略某些文件

一般我们总会有些文件无需纳入 Git 的管理，也不希望它们总出现在未跟踪文件列表。通常都是些自动生成的文件，比如日志文件，或者编译过程中创建的临时文件等。我们可以创建一个名为 `.gitignore` 的文件，列出要忽略的文件模式。来看一个实际的例子：

```
$ cat .gitignore
*.[oa]
*~
```

第一行告诉 Git 忽略所有以 `.o` 或 `.a` 结尾的文件。一般这类对象文件和存档文件都是编译过程中出现的，我们用不着跟踪它们的版本。第二行告诉 Git 忽略所有以波浪符（`~`）结尾的文件，许多文本编辑软件（比如 Emacs）都用这样的文件名保存副本。此外，你可能还需要忽略 `log`，`tmp` 或者 `pid` 目录，以及自动生成的文档等等。要养成一开始就设置好 `.gitignore` 文件的习惯，以免将来误提交这类无用的文件。

文件 `.gitignore` 的格式规范如下：

* 所有空行或者以注释符号 `＃` 开头的行都会被 Git 忽略。
* 可以使用标准的 glob 模式匹配。
* 匹配模式最后跟反斜杠（`/`）说明要忽略的是目录。
* 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（`!`）取反。

所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。星号（`*`）匹配零个或多个任意字符；`[abc]` 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（`?`）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如 `[0-9]` 表示匹配所有 0 到 9 的数字）。

我们再看一个 `.gitignore` 文件的例子：

```
# 此为注释 – 将被 Git 忽略
# 忽略所有 .a 结尾的文件
*.a

# 但 lib.a 除外
!lib.a

# 仅仅忽略项目根目录下的 TODO 文件，不包括 subdir/TODO
/TODO

# 忽略 build/ 目录下的所有文件
build/

# 会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
doc/*.txt

# ignore all .txt files in the doc/ directory
doc/**/*.txt
```

A `**/` pattern is available in Git since version 1.8.2.

### 查看以暂存和为暂存的更新

```
// 比较工作目录中当前文件和暂存区域快照之间的差异，也就是修改之后还没有暂存起来的变化内容。
// 暂存前后变化
$ git diff

// 已经暂存起来的文件和上次提交时的快照之间的差异
// 已经暂存起来的变化
$ git diff --cached 或 $git diff --staged(Git 1.6.1及更高版本)
```

### 提交更新

```
git commit
git commit -m "说明"
```

### 跳过使用暂存区域

    // Git会自动把所有`已跟踪文件`暂存起来一并提交
    git commit -a -m "说明"

### 移除文件

要从 Git 中移除某个文件，就必须要从已跟踪文件清单中移除（确切地说，是从暂存区域移除），然后提交。可以用 `git rm` 命令完成此项工作，并连带从工作目录中删除指定的文件，这样以后就不会出现在未跟踪文件清单中了。

如果只是简单地从工作目录中手工删除文件，运行 `git status` 时就会在 “Changes not staged for commit” 部分（也就是_未暂存_清单）看到：

```
$ rm grit.gemspec
$ git status
On branch master
Changes not staged for commit:
 (use "git add/rm <file>..." to update what will be committed)
 (use "git checkout -- <file>..." to discard changes in working directory)

 deleted: grit.gemspec

no changes added to commit (use "git add" and/or "git commit -a")
```

然后再运行 `git rm` 记录此次移除文件的操作：

```
$ git rm grit.gemspec
rm 'grit.gemspec'

$ git status
On branch master
Changes to be committed:
 (use "git reset HEAD <file>..." to unstage)

 deleted: grit.gemspec
```

最后提交的时候，该文件就不再纳入版本管理了。如果删除之前修改过并且已经放到暂存区域的话，则必须要用强制删除选项 `-f`（译注：即 force 的首字母），以防误删除文件后丢失修改的内容。

另外一种情况是，我们想把文件从 Git 仓库中删除（亦即从暂存区域移除），但仍然希望保留在当前工作目录中。换句话说，仅是从跟踪清单中删除。比如一些大型日志文件或者一堆 `.a` 编译文件，不小心纳入仓库后，要移除跟踪但不删除文件，以便稍后在 `.gitignore` 文件中补上，用 `--cached` 选项即可：

```
$ git rm --cached readme.txt
```

后面可以列出文件或者目录的名字，也可以使用 glob 模式。比方说：

```
$ git rm log/\*.log
```

注意到星号 `*` 之前的反斜杠 `\`，因为 Git 有它自己的文件模式扩展匹配方式，所以我们不用 shell 来帮忙展开（译注：实际上不加反斜杠也可以运行，只不过按照 shell 扩展的话，仅仅删除指定目录下的文件而不会递归匹配。上面的例子本来就指定了目录，所以效果等同，但下面的例子就会用递归方式匹配，所以必须加反斜杠。）。此命令删除所有 `log/` 目录下扩展名为 `.log` 的文件。类似的比如：

```
$ git rm \*~
```

会递归删除当前目录及其子目录中所有 `~` 结尾的文件。

### 移动文件

不像其他的 VCS 系统，Git 并不跟踪文件移动操作。如果在 Git 中重命名了某个文件，仓库中存储的元数据并不会体现出这是一次改名操作。不过 Git 非常聪明，它会推断出究竟发生了什么，至于具体是如何做到的，我们稍后再谈。

既然如此，当你看到 Git 的 `mv` 命令时一定会困惑不已。要在 Git 中对文件改名，可以这么做：

```
$ git mv file_from file_to
```

它会恰如预期般正常工作。实际上，即便此时查看状态信息，也会明白无误地看到关于重命名操作的说明：

```
$ git mv README.txt README
$ git status
On branch master
Changes to be committed:
 (use "git reset HEAD <file>..." to unstage)

 renamed: README.txt -> README
```

其实，运行 `git mv` 就相当于运行了下面三条命令：

```
$ mv README.txt README
$ git rm README.txt
$ git add README
```

如此分开操作，Git 也会意识到这是一次改名，所以不管何种方式都一样。当然，直接用 `git mv` 轻便得多，不过有时候用其他工具批处理改名的话，要记得在提交前删除老的文件名，再添加新的文件名。

## 查看提交历史

    // 按提交时间列出所有更新，最近的更新排在最上面。
    $ git log

    // `-p`选项展开显示每次提交的内容差异，`-2`表示仅显示最近的两次更新
    $ git log -p -2

    // 单词层面的对比
    // 新增加的单词被 {+ +} 括起来，被删除的单词被 [- -] 括起来。
    $ git log -U1 --word-diff

    // 显示简要的整改行数统计
    $ git log --stat

    // 显示一行
    $ git log --pretty=oneline

    // 自定义格式
    $ git log --pretty=format:"%h - %an, %ar : %s"

表 2-1 列出了常用的格式占位符写法及其代表的意义。

| 选项 | 说明 |
| --- | --- |
| %H | 提交对象（commit）的完整哈希字串 |
| %h | 提交对象的简短哈希字串 |
| %T | 树对象（tree）的完整哈希字串 |
| %t | 树对象的简短哈希字串 |
| %P | 父对象（parent）的完整哈希字串 |
| %p | 父对象的简短哈希字串 |
| %an | 作者（author）的名字 |
| %ae | 作者的电子邮件地址 |
| %ad | 作者修订日期（可以用 -date= 选项定制格式） |
| %ar | 作者修订日期，按多久以前的方式显示 |
| %cn | 提交者\(committer\)的名字 |
| %ce | 提交者的电子邮件地址 |
| %cd | 提交日期 |
| %cr | 提交日期，按多久以前的方式显示 |
| %s | 提交说明 |


一些其他常用的选项及其释义。

| 选项 | 说明 |
| --- | --- |
| -p | 按补丁格式显示每个更新之间的差异。 |
| --word-diff | 按 word diff 格式显示差异。 |
| --stat | 显示每次更新的文件修改统计信息。 |
| --shortstat | 只显示 --stat 中最后的行数修改添加移除统计。 |
| --name-only | 仅在提交信息后显示已修改的文件清单。 |
| --name-status | 显示新增、修改、删除的文件清单。 |
| --abbrev-commit | 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。 |
| --relative-date | 使用较短的相对时间显示（比如，“2 weeks ago”）。 |
| --graph | 显示 ASCII 图形表示的分支合并历史。 |
| --pretty | 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）。 |
| --oneline | `--pretty=oneline --abbrev-commit` 的简化用法。 |

其他常用的类似选项。

| 选项 | 说明 |
| --- | --- |
| -\(n\) | 仅显示最近的 n 条提交 |
| --since, --after | 仅显示指定时间之后的提交。 |
| --until, --before | 仅显示指定时间之前的提交。 |
| --author | 仅显示指定作者相关的提交。 |
| --committer | 仅显示指定提交者相关的提交。 |

来看一个实际的例子，如果要查看 Git 仓库中，2008 年 10 月期间，Junio Hamano 提交的但未合并的测试脚本（位于项目的 t\/ 目录下的文件），可以用下面的查询命令：

```
$ git log --pretty="%h - %s" --author=gitster --since="2008-10-01" \
 --before="2008-11-01" --no-merges -- t/

5610e3b - Fix testcase failure when extended attribute
acd3b9e - Enhance hold_lock_file_for_{update,append}()
f563754 - demonstrate breakage of detached checkout wi
d1a43f2 - reset --hard/read-tree --reset -u: remove un
51a94af - Fix "checkout --track -b newbranch" on detac
b0ad11e - pull: allow "git pull origin $something:$cur
```

Git 项目有 20,000 多条提交，但我们给出搜索选项后，仅列出了其中满足条件的 6 条。



### 使用图形化工具查阅提交历史

有时候图形化工具更容易展示历史提交的变化，随 Git 一同发布的 gitk 就是这样一种工具。它是用 Tcl\/Tk 写成的，基本上相当于 `git log` 命令的可视化版本，凡是 `git log` 可以用的选项也都能用在 gitk 上。在项目工作目录中输入 gitk 命令后，就会启动图 2-2 所示的界面。

![](http://git-scm.com/figures/18333fig0202-tn.png)

图 2-2. gitk 的图形界面

上半个窗口显示的是历次提交的分支祖先图谱，下半个窗口显示当前点选的提交对应的具体差异。




