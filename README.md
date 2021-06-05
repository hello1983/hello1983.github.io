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

`yum install docker-compose`

#### 启动Docker

`systemctl start docker`

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

##### 以下载 Docker Compose 

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


