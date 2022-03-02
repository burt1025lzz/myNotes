### 国内服务器搭建 openvpn

#### 1. 查看服务器内核版本

```shell
lsb_release -a
```

#### 2. 下载对应版本的 clash

```shell
https://github.com/Dreamacro/clash/releases
```

#### 3. 解压文件

```shell
gzip -d clash-linux-amd64-v1.8.0.gz  # 解压
mv clash-linux-amd64-v1.8.0 clash  # 重命名
chmod 777 clash  # 添加可执行权限
```

以下方式 2 选一
------

------

#### 4. 直接使用

###### 1. 上传 clash 配置

要重新命名成 config.yaml

###### 2. 运行 clash

```shell
bash ./clash -d .
```

###### 3. 新建终端

------

#### 4. 使用 pm2

###### 1. 安装node.js 环境

```shell
cd /opt/
wget https://nodejs.org/dist/v14.0.0/node-v14.0.0-linux-x64.tar.xz
tar xvf node-v14.0.0-linux-x64.tar.xz
# 添加到环境变量
echo "export NODE_HOME=/opt/node-v14.0.0-linux-x64" >> ~/.bashrc
echo "export PATH=\$NODE_HOME/bin:\$PATH" >> ~/.bashrc
source ~/.bashrc
```

###### 2. 全局安装 pm2

```shell
npm install pm2 -g
```

###### 3. 上传 clash 配置

要重新命名成 config.yaml

###### 4. 运行 clash

```shell
cd ~ # 回到 clash 目录
touch start_clash.sh  # 新建 start_clash.sh
chmod 777 start_clash.sh  # 添加可执行权限
echo "./clash -d ." > start_clash.sh  # 写入命令
pm2 start start_clash.sh # 运行
pm2 list  # 查看运行状态
```

------

#### 5. 对当前终端开启代理

```shell
export https_proxy=http://127.0.0.1:7890 http_proxy=http://127.0.0.1:7890 all_proxy=socks5://127.0.0.1:7891
```

##### 6. 安装 openvpn 脚本

```shell
wget https://git.io/vpn -O openvpn-install.sh && bash openvpn-install.sh
```

如果自动获取 ip 失败，第一处输入自己的公网 ip 就可以。

