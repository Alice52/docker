## mysql

1. images
   - dev-mysql-standalone
   - dev-mysql-master
   - dev-mysql-slave

2. compare
   - master/slave has more `mysql.cnf` files than standalone
   - master and slave are only different from the `mysql.cnf` about `server_id/relay_log`

## deploy msater-slave mode step

1. master: logs, grant, and backup data

    ```sql
    -- 1. flush log
    flush logs;
    -- 2. grant slave permission to slave
    grant replication slave on *.* to 'username'@'%' identified by '123456';
    FLUSH PRIVILEGES;
    ```

    ```sql
    -- 1. frozen master data
    mysql> flush tables with read lock;
    -- 2. new terminal and backup data
    mysqldump -h 127.0.0.1 -uroot -proot --skip-comments --databases --compact -C -q -f db1 db2  db3 >> back.sql
    -- 3. obtain master bin-log postion
    mysql> show master status;
    -- 4. unfrozen master data
    mysql> unlock tables;
    ```

2. slave

    ```sql
     -- 1. import data from backup
    $ mysql -uroot -proot <back.sql
    -- 2. set connection to master with bin-log position
    CHANGE MASTER TO MASTER_HOST='172.18.135.185', MASTER_PORT=3306, MASTER_USER='repl', MASTER_PASSWORD='repl', MASTER_LOG_FILE='mysql-bin.000028', MASTER_LOG_POS=4032;
    -- 3. enable slave
    mysql> start slave;
    -- 4. check slave status
    mysql> show slave status\G;
        -- Slave_IO_Running: Yes
        -- Slave_SQL_Running: Yes
    -- 5. set slave read only
    SET GLOBAL READ_ONLY=1;
    SET GLOBAL SUPER_READ_ONLY=ON;
    ```
