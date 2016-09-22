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


