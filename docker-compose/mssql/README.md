## 使用步骤
1. 修改 `docker-compose.yml ` 文件内容。
2. Create volume _vol-mssql_.

    ```
    mkdir -p /home/mssql/mssql-vol/
    docker volume create --opt type=none --opt device=/home/mssql/mssql-vol --opt o=bind --name=mssql-vol
    ```
3. 在 `docker-compose.yml ` 文件所在目录下执行如下命令：

    ```
    docker-compose up -d
    ```
[link](https://dashboard.daocloud.io/packages/487751ba-45ef-49d6-833a-490dfaa5e08b)
