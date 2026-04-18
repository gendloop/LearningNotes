# Guide

## wsl2下安装

```bash
# 更新源
$ sudo apt update

# 安装zsh
sudo apt install zsh -y

# 安装ohmyzsh
git clone https://github.com/gendloop/ohmyzsh  ${ZSH:-~/.oh-my-zsh}

# 复制配置文件
cp ${ZSH:-~/.oh-my-zsh}/templates/.zshrc ~/.zshrc

# 查看可用shell
cat /etc/shells

# 设置zsh为默认shell
chsh -s $(which zsh)

# 查看当前shell
echo $SHELL
```
