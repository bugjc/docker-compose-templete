
## 1. 创建 MySQL容器
```
docker run --restart=always --name ea-mysql -p 3306:3306 -v /data/mysql:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d  daocloud.io/mysql
```
- --restart 表示重启的策略
- -p 代表端口映射，格式为：宿主机映射端口:容器运行端口
- -e 代表添加环境变量，MYSQL_ROOT_PASSWORD是root用户的登陆密码
- -v 代表绑定挂载目录，格式为：宿主机目录:容器目录
#### 重启策略参数
- no，默认策略，在容器退出时不重启容器
- on-failure，在容器非正常退出时（退出状态非0），才会重启容器
- on-failure:3，在容器非正常退出时重启容器，最多重启3次
- always，在容器退出时总是重启容器
- unless-stopped，在容器退出时总是重启容器，但是不考虑在Docker守护进程启动时就已经停止了的容器


## 2. 进入 MySQL 容器,登陆 MySQL

```
# 进入 mysql 容器
docker exec -it ea-mysql /bin/bash

# 登录 mysql
mysql -u root -p
```

## 3. 常见问题

#### （1）客户端连接不上，Navicat 报 1251 或 SQLyog 报 2058 错误。
解决方式：更改加密规则以及更新root用户密码。原因是客户端只支持旧版的加密。

```mysql
# 1.容器中登录mysql,查看mysql的版本
mysql> status;

# 2.进行授权远程连接(注意mysql 8.0跟之前的授权方式不同)
mysql> GRANT ALL ON *.* TO 'root'@'%';
mysql> flush privileges;

# 3.更改加密规则
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'password' PASSWORD EXPIRE NEVER;

# 4.更新root用户密码
mysql> ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
mysql> flush privileges;
```
