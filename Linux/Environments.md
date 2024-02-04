# Environments

## JDK 8

yum install java-1.8.0-openjdk* -y

## MySQL 5.7

1. 下载 MySQL yum 包

   ```bash
   wget http://repo.mysql.com/mysql57-community-release-el7-10.noarch.rpm
   ```

2. 安装 MySQL 源

   ```bash
   rpm -Uvh mysql57-community-release-el7-10.noarch.rpm
   rpm --import https://repo.mysql.com/RPM-GPG-KEY-mysql-2022
   ```

3. 安装 MySQL 服务端

   ```bash
   yum install -y mysql-community-server
   ```

4. 启动 MySQL

   ```bash
   systemctl start mysqld
   ```

5. 检查是否启动成功

   ```bash
   systemctl status mysqld
   ```

6. 获取临时密码

   ```bash
   grep 'temporary password' /var/log/mysqld.log 
   ```

7. 通过临时密码登录 MySQL，配置密码规则，修改 root 密码

   ```bash
   mysql -uroot -p
   mysql> set global validate_password_policy=0;
   mysql> set global validate_password_length=1;
   ```

8. 授权远程用户登录

   ```mysql
   GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpassword' WITH GRANT OPTION;
   FLUSH PRIVILEGES;
   ```

9. 开启开机自启动

   ```bash
   systemctl enable mysqld
   systemctl daemon-reload
   ```

10. 配置 MySQL 的配置文件 my.cnf

11. 重启 MySQL，使配置文件生效

    ```bash
    service mysqld restart
    ```

12. 防火墙开放 MySQL 的默认端口 3306

    ```bash
    firewall-cmd --state
    firewall-cmd --zone=public --add-port=3306/tcp --permanent
    firewall-cmd --reload
    ```

13. 卸载MySQL仓库

    ```bash
    rpm -qa | grep mysql
    yum -y remove mysql57-community-release-el7-10.noarch
    ```

## Redis

1. `yum install -y epel-release`

2. `yum install -y redis`

3. `systemctl start redis`

   `systemctl stop redis`

   `systemctl status redis`

   `systemctl enable redis`

4. 修改配置文件 `/etc/redis.conf`：port、requirepass、bind 等

## Docker

1. 安装依赖

   ```bash
   yum install -y yum-utils device-mapper-persistent-data lvm2
   ```

2. 设置 yum 源

   ```bash
   yum-config-manager --add-repo http://download.docker.com/linux/centos/docker-ce.repo（中央仓库）
   
   yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo（阿里仓库）
   ```

3. 选择 Docker 版本并安装

   ```bash
   yum list docker-ce --showduplicates | sort -r
   yum -y install docker-ce-18.06.3.ce
   ```

4. 启动 Docker 并设置开机自启

   ```bash
   systemctl start docker
   systemctl enable docker
   ```

   

   