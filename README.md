# repo

## 关于

The Slackware Linux CN Community Repository.

这里是Slackware Linux 中文社区的SlackBuilds 仓库，存放本社区所贡献的SlackBuilds。

如果你想在这里加入你的[SlackBuild](http://docs.slackware.com/slackware:slackbuild_scripts)，请阅读我们的[slackbuild-guidelines](https://github.com/slackwarecn/slackbuild-guidelines)。

当你提交完一个符合上述guidelines 的SlackBuild 后，请[提交Issue](https://github.com/slackwarecn/repo/issues) 并写明你的SlackBuild 所对应的项目名称。

## 使用

### 克隆该仓库

```bash
git clone https://github.com/slackwarecn/repo.git
cd repo
```

### 初始化SlackBuilds

```bash
./sbm init
```

至此你已经获得了所有的SlackBuilds。

### 构建SlackBuilds

例子如下。

```bash
./sbm build dbus-python3 extra-cmake-modules
```

如果你只是想单纯使用SlackBuild，请忽略下一节。

## 管理

### 设置GPG KEY

```bash
git config user.signingkey <key ID>
gpg --fingerprint <key ID> | perl -nE '$.-2 or s/^\h+// and print' | tee -a fingerprint
uniq -d fingerprint | tr -s "\n" | sort -o fingerprint
```

> 关于在GIT 中使用GPG 签名更多信息可以参考[这里](http://arondight.me/2016/04/17/%E4%BD%BF%E7%94%A8GPG%E7%AD%BE%E5%90%8DGit%E6%8F%90%E4%BA%A4%E5%92%8C%E6%A0%87%E7%AD%BE/)。

### SlackBuild Manager

在本项目中，SlackBuild 由`git-submodule` 的形式存放，也就意味着每个SlackBuild 都对应一个GIT 仓库。

项目中提供一个脚本[`sbm`](sbm) 来管理这些SlackBuild（或者说GIT 子模块），你可以使用`help` 参数运行`sbm` 来查看更多信息。

```bash
./sbm help
```

> `sbm` 的管理动作只能工作在干净的GIT 仓库中。

### 添加SlackBuilds

例子如下。

```bash
./sbm add netease-cloud-music shadowsocks-qt5 \
          https://github.com/slackwarecn-slackbuilds/fcitx-rime-slackbuild
vim Changes
git add .
git commit -S

```

### 删除SlackBuilds

例子如下。

```bash
./sbm del netease-cloud-music shadowsocks-qt5 fcitx-rime-slackbuild
vim Changes
git add .
git commit -S
```

### 同步/更新SlackBuilds

例子如下。

```bash
./sbm sync
vim Changes
git add .
git commit -S
```

### 撤销所有更改

例子如下。

```bash
./sbm undo
```

### 推送上游

例子如下。

```bash
git push origin master
```

> 不支持Pull Request。

