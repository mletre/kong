# kong Install in VM Server


## Local setup

Before your start the configuration you must installed kong in the server by this way. In the tutorial using Debian 12 Bookworm.

- Update & Upgrade the System
```shell
sudo apt update && sudo apt upgrade
```

- Download DEB Package from the konghq
```shell
curl -Lo kong-3.8.0.deb "https://packages.konghq.com/public/gateway-38/deb/debian/pool/bullseye/main/k/ko/kong_3.8.0/kong_3.8.0_$(dpkg --print-architecture).deb"
```

- Install
```shell
sudo apt install -y ./kong-3.8.0.deb
```

Prepare Postgresql Databases.

- Install Postgresql and other tools
```shell
sudo apt install git postgresql net-tools
```

- Change to the root user
```shell
sudo su
cd /root/
```

- Make user and database for kong
```shell
su - postgres
psql
CREATE USER kong WITH PASSWORD 'super_secret'; CREATE DATABASE kong OWNER kong;
quit
```

- Clone the git repository
```shell
git clone https://github.com/mletre/kong.git
```

- Change Directory
```shell
cd kong/install/on-vm
```

- Copy The configuration
```shell
cp kong.conf /etc/kong/
```

- Start The Kong Migration Databases
```shell
kong migrations bootstrap -c /etc/kong/kong.conf
```

- Start the Kong
```shell
kong start -c /etc/kong/kong.conf
```

- Check The Running Port
```shell
root@machine:~# netstat -tulpn
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.0.1:8444          0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 127.0.0.1:8444          0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      482/sshd: /usr/sbin
tcp        0      0 0.0.0.0:8443            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8443            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8445            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8000            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8001            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8001            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:8002            0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 0.0.0.0:5432            0.0.0.0:*               LISTEN      491/postgres
tcp        0      0 127.0.0.1:45397         0.0.0.0:*               LISTEN      481/containerd
tcp        0      0 127.0.0.1:8007          0.0.0.0:*               LISTEN      735/nginx: master p
tcp        0      0 127.0.0.1:8007          0.0.0.0:*               LISTEN      735/nginx: master p
tcp6       0      0 :::22                   :::*                    LISTEN      482/sshd: /usr/sbin
tcp6       0      0 :::5432                 :::*                    LISTEN      491/postgres
udp        0      0 0.0.0.0:68              0.0.0.0:*                           440/dhclient
root@machine:~#

```

- Done

## Source

- https://docs.konghq.com/gateway/3.8.x/install/linux/debian/?install=oss
- https://docs.konghq.com/gateway/latest/install/post-install/set-up-data-store/
