# CC Switch for Ubuntu 安装指南

##### 参考链接

代码仓地址：https://github.com/farion1231/cc-switch



## 第一步：下载并安装

```shell
wget https://github.com/farion1231/cc-switch/releases/download/v3.10.3/CC-Switch-v3.10.3-Linux-x86_64.deb

sudo dpkg -i CC-Switch-v3.10.3-Linux-x86_64.deb

# 自动修复所有缺失依赖
sudo apt -f install -y

# 验证安装是否成功
dpkg -l | grep cc-switch

pkill -9 cc-switch

```



## 第二步：修复界面乱码问题

启动后如果看到方框或乱码，是系统缺少中文字体导致的，执行以下命令修复

```bash
# 安装中文字体
sudo apt install -y fonts-wqy-microhei fonts-wqy-zenhei fonts-noto-cjk fonts-noto-color-emoji

# 强制关闭 CC Switch
pkill -9 cc-switch

# 刷新字体缓存
fc-cache -fv

# 重新启动
cc-switch
```



