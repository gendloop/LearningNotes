# Guide

## wsl2下安装

```bash
# 更新源
$ sudo apt update
# 安装Zsh
sudo apt install zsh -y
# 安装OhMyZsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
# 查看可用shell
cat /etc/shells
# 设置zsh为默认shell
chsh -s $(which zsh)
# 查看当前shell
echo $SHELL
```

## 配置

```bash
# 编辑配置
vim ~/.zshrc
```
