#### 1. Shadowsocks 一键安装管理脚本

```shell
wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ss-go.sh && chmod +x ss-go.sh && bash ss-go.sh
```

#### Docker 安装

```shell
curl -sSL https://get.docker.com/ | sh

curl https://get.docker.com -fsSL | sh
```

#### 2. Docker-compose 安装

```shell
yum install docker-compose
```

#### 启动Docker

```shell
systemctl enable --now docker
```

### 3. Snell-Docker搭建

####  拉取镜像

```docker
docker pull primovist/snell-docker
```

####  HTTP

```bash
docker run -d --env PORT=12543 --env PSK=dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg --env OBFS=http -p 12543:12543 -p 12543:12543/udp --name snell-server -v /etc/snell/:/etc/snell/ --restart=always primovist/snell-docker
```
  端口 `12543`
  
  SERVER_PORT为端口自定义端口CONFIG为自定义配置文件位置
  
  PSK_KEYS为自定义`PSK`
  
  CONFIG_DIR为自定义配置文件目录
  
  OBFS=后可改为`http`

#### TLS

```bash
docker run -d --env PORT=12543 --env PSK=dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg --env OBFS=tls -p 12543:12543 -p 12543:12543/udp --name snell-server -v /etc/snell/:/etc/snell/ --restart=always primovist/snell-docker
```

   端口 `12543`
   
   PSK为dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg
   
   配置文件目录为/etc/snell/
   
   OBFS为 `tls`

#### 4.Compose 安装

##### 下载 Docker Compose 

```shell
sudo curl -L "https://github.com/docker/compose/releases/download/1.24.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
```
##### 执行权限

```shell
sudo chmod +x /usr/local/bin/docker-compose
```
##### 创建软链

```shell
sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
##### 测试是否安装成功

```shell
docker-compose --version
```

#### 5. CentOS  WARP作为出口

```shell
mkdir wgcf

cd wgcf

wget -O wgcf https://github.com/ViRb3/wgcf/releases/download/v2.2.3/wgcf_2.2.3_linux_amd64

# 或者使用本站镜像（同时支持ipv6与ipv4）

wget -O wgcf https://btpanel.loukky.com/wgcf/wgcf_2.2.3_linux_amd64

chmod +x wgcf
```
##### 初次使用需要注册用户并生成配置文件：

```shell
./wgcf register

./wgcf generate
```
centos7可以使用以下命令安装：

```shell

yum install epel-release elrepo-release

yum install yum-plugin-elrepo

yum install kmod-wireguard wireguard-tools

```
##### 把刚刚下载好的配置文件wgcf-profile.conf上传至/etc/wireguard，然后修改下配置文件，其中DNS建议同时添加上IPV4与IPV6的DNS，这里使用的Cloudflare的DNS。

```shell

For IPv4: 1.1.1.1 and 1.0.0.1

For IPv6: 2606:4700:4700::1111 and 2606:4700:4700::1001
```

##### 同时记得如果需要cf warp的IPV6就删掉 AllowedIPs = 0.0.0.0/0

##### 如果需要cf warp的ipv4就删掉 AllowedIPs = ::/0

#### 安装好以后记得重启下VPS。

#### 记住不要两个同时启用，不然会导致你vps原本的ip地址无法连接上去

##### 最后保存配置文件，修改文件名为wgcf.conf 然后继续：

```shell
#加载内核模块

modprobe wireguard

#检查WG模块加载是否正常

lsmod | grep wireguard

# 最后开关隧道的命令为：

#开启隧道

sudo wg-quick up wgcf

#关闭隧道

sudo wg-quick down wgcf

```
