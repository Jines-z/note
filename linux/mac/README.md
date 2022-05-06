## Mac 开发环境搭建教程

1、安装 Homebrew
```shell script
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install.sh)"
```
国内站点安装：
```shell script
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

2、安装 Git、Yarn、Tterm2
```shell script
brew install git
brew install yarn
brew install iterm2
```

3、安装 NVM
```shell script
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
```
添加配置文件：创建 ~/.zshrc 文件，然后将下面代码复制到文件中，并保存。
```shell script
export NVM_DIR= " $( [ -z  " ${XDG_CONFIG_HOME-} " ] &&  printf %s " ${HOME} /.nvm "  ||  printf %s " ${XDG_CONFIG_HOME} /nvm " ) " 
[ -s  " $ NVM_DIR /nvm.sh " ] &&  \.  " $NVM_DIR /nvm.sh "
```
M1 芯片安装 node@15.14.0 以下版本时，需要进入 Rosetta2 模式，打开命令行执行：
```shell script
arch -x86_64 zsh
```

4、安装 oh-my-zsh
```shell script
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
sh -c "$(curl -fsSL https://gitee.com/mirrors/oh-my-zsh/raw/master/tools/install.sh)"
```
安装 plugin zsh-autosuggestions
```shell script
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
source ~/.zsh/zsh-autosuggestions/zsh-autosuggestions.zsh

```

5、安装 Mos 平滑鼠标和 Alt-Tab 切换
-   Mos Github：[https://github.com/Caldis/Mos](https://github.com/Caldis/Mos)
-   Alt-Tab Github：[https://github.com/lwouis/alt-tab-macos](https://github.com/lwouis/alt-tab-macos)

6、安装 Wondershare Dr.Fone

更多 Mac 周边技巧：[https://github.com/hzlzh/Best-App](https://github.com/hzlzh/Best-App)

[目录](https://github.com/jines-z/note)
