# repo

## 关于

The Slackware Linux CN Community Repository.

这里是 Slackware Linux 中文社区的 SlackBuilds 仓库，存放本社区所贡献的 SlackBuilds。

如果你想在这里加入你的[SlackBuild](http://docs.slackware.com/slackware:slackbuild_scripts)，请阅读我们的[slackbuild-guidelines](https://github.com/slackwarecn/slackbuild-guidelines)。

当你提交完一个符合上述 guidelines 的 SlackBuild 后，请[提交 Issue](https://github.com/slackwarecn/repo/issues) 并写明你的 SlackBuild 所对应的项目名称。

## 使用

### 克隆该仓库

```bash
git clone https://github.com/slackwarecn/repo.git
cd repo
```

### 初始化 SlackBuilds

```bash
./sbm init
```

至此你已经获得了所有的 SlackBuilds。

### 构建 SlackBuilds

```bash
./sbm build dbus-python3 extra-cmake-modules
```

如果你只是想单纯使用 SlackBuild，请忽略下一节。

## 管理

### 设置 GPG KEY

```bash
git config user.signingkey <key ID>
gpg --fingerprint <key ID> | perl -nE '$.-2 or s/^\h+// and print' | tee -a fingerprint
uniq -d fingerprint | tr -s "\n" | sort -o fingerprint
```

> 关于在 GIT 中使用 GPG 签名更多信息可以参考[这里](http://arondight.me/2016/04/17/%E4%BD%BF%E7%94%A8GPG%E7%AD%BE%E5%90%8DGit%E6%8F%90%E4%BA%A4%E5%92%8C%E6%A0%87%E7%AD%BE/)。

### SlackBuild Manager

在本项目中，SlackBuild 由`git-submodule` 的形式存放，也就意味着每个 SlackBuild 都对应一个 GIT 仓库。

项目中提供一个脚本[`sbm`](sbm) 来管理这些 SlackBuild（或者说 GIT 子模块），你可以使用`help` 参数运行`sbm` 来查看更多信息。

```bash
./sbm help
```

> `sbm` 的管理动作只能工作在干净的 GIT 仓库中。

### 添加 SlackBuilds

```bash
./sbm add netease-cloud-music shadowsocks-qt5 \
          https://github.com/slackwarecn-slackbuilds/fcitx-rime-slackbuild
vim Changes
git add .
git commit -S

```

### 删除 SlackBuilds

```bash
./sbm del netease-cloud-music shadowsocks-qt5 fcitx-rime-slackbuild
vim Changes
git add .
git commit -S
```

### 同步、更新 SlackBuilds

```bash
./sbm sync
vim Changes
git add .
git commit -S
```

### 撤销所有更改

```bash
./sbm undo
```

### 推送上游

```bash
git push origin master
```

## 许可

[MIT LICENSE](LICENSE) 。
