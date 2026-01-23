

# Configuring MySQL Servers dans ProxySQL
```
INSERT INTO mysql_servers(hostgroup_id, hostname, port)
VALUES
(0, '10.10.20.20', 3306),  -- master
(1, '10.10.20.21', 3306);  -- slave
(1, '10.10.20.22', 3306);  -- slave


LOAD MYSQL SERVERS TO RUNTIME;
SAVE MYSQL SERVERS TO DISK;

```
# MysQL User pour ProxySQL sur le serveur MySQL

```
CREATE USER 'user'@'172.16.30.54' IDENTIFIED BY 'projetnuez2026';
GRANT ALL PRIVILEGES ON *.* TO 'user'@'172.16.30.54';
FLUSH PRIVILEGES;
```
# Puis dans proxysql on ajoute l'utilisateur mysql pour se connecter aux serveurs mysql via proxysql
```
INSERT INTO mysql_users(username, password, default_hostgroup)
VALUES ('user', 'projetnuez2026', 1);

LOAD MYSQL USERS TO RUNTIME;
SAVE MYSQL USERS TO DISK;
```