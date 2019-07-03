# 在 LINUX 安装 ORACLE SQLPLUS 客户端



> Sqlplus 是与 Oracle 数据库服务端进行交互的客户端工具
>
> Linux 下安装客户端需要
>
> - ORACLE 客户端安装包（采用 RPM）
> - 系统ROOT用户

## 1 获取安装包

- 1.1 在 ORACLE 官方网站，下载 ORACLE 客户端基础包、SQLPLUS 包：

```shell
oracle-instantclient-basic.rpm
oracle-instantclient-sqlplus.rpm
```

- 1.2 将安装包传输给 Linux 下

> 可以采用 pscp 等命令

## 2 安装

- 2.1 进入 ROOT 用户 ( ` sudo su` )后执行 rpm 包安装命令：

  ```shell
  rpm -ivh oracle-instantclient-basic.rpm
  rpm -ivh oracle-instantclient-sqlplus.rpm
  ```

- 2.2 安装完成后，上述程序会自动生成客户端目录 `/usr/lib/oracle/client64`，其中 bin、lib 目录分别是可 Oracle 客户端的执行文件和连接库

- 2.3 在`/usr/lib/oracle/client64`目录下，用 vim 等文本编辑命令，创建并配置 Oracle客户端的网络服务名配置文件tnsnames.ora

  ```shell
  vim /usr/lib/oracle/client64/tnsnames.ora
  
  
  
  DB =  
  (DESCRIPTION =  
  (ADDRESS_LIST =  
  (ADDRESS = (PROTOCOL = TCP)(HOST = 0.0.0.0)(PORT = 1521))  
  )  
   
  (CONNECT_DATA = 
  (SID = DBSID)  
  (SERVER = DEDICATED)  
  ) 
  )
  
  
  ```

- 2.4 登录 sqlplus 使用用户，在`.bashrc` （ Linux 系统的环境变量配置文件）中设置 ORACLE 客户端环境变量：

  ```shell
  export ORACLE_HOME=/usr/lib/oracle/client64
  export TNS_ADMIN=/usr/lib/oracle/client64
  export LD_LIBRARY_PATH=/usr/lib/oracle/client64/lib
  ```

- 2.5 在`.bashrc`中，将 sqlplus 所在的路径添加到 PATH 环境变量中：

  ```shell
  export ORABIN=/usr/lib/oracle/client64/bin
  PATH=$PATH:$ORABIN
  export PATH
  ```

- 2.6 完成安装后，可以在命令窗口用 sqlplus 命令来操作远程数据库了。