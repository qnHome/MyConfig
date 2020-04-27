# MyConfig

# zsh
```
# 更新
sudo apt update
# 安装
sudo apt install zsh
# 查看版本
zsh --version
# 设置默认shell
whereis zsh
sudo usermod -s [上面的路径] $(whoami)
# 集成 oh-my-zsh
sudo apt install git
sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```
