

### 1. ss-go安装
* Shadowsocks 一键安装管理脚本

`wget -N --no-check-certificate https://raw.githubusercontent.com/ToyoDAdoubi/doubi/master/ss-go.sh && chmod +x ss-go.sh && bash ss-go.sh`

### 2. Docker 安装

`curl -sSL https://get.docker.com/ | sh`

`curl https://get.docker.com -fsSL | sh`

* Docker-compose 安装

`yum install docker-compose`

* 启动Docker

`systemctl start docker`

### 3.Snell-Docker搭建

####  拉取镜像

```docker
docker pull primovist/snell-docker
```

####  `HTTP`

```bash
docker run -d --env PORT=12543 --env PSK=dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg --env OBFS=http -p 12543:12543 -p 12543:12543/udp --name snell-server -v /etc/snell/:/etc/snell/ --restart=always primovist/snell-docker
```

##### 其中

- 端口 `12543`
- SERVER_PORT为端口自定义端口CONFIG为自定义配置文件位置
- PSK_KEYS为自定义`PSK`
- CONFIG_DIR为自定义配置文件目录
- OBFS=后可改为`http`

#### `TLS`

```bash
docker run -d --env PORT=12543 --env PSK=dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg --env OBFS=tls -p 12543:12543 -p 12543:12543/udp --name snell-server -v /etc/snell/:/etc/snell/ --restart=always primovist/snell-docker
```

##### 其中

- 端口 `12543`
- PSK为dFDL0H4NFMOieRyeb6Ly59EJUwrCiEg
- 配置文件目录为/etc/snell/
- OBFS为 `tls`
