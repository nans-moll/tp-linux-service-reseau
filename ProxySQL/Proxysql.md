### le rôle de ce service est de répartir les requêtes faites vers le serveur de base de donnée et de créer un cluster natif (voir galera) afin d'assurer la continuité de service sur ceux-ci. Ce service est essentiel pour ne pas surcharger les serveurs et assurer une continuité fluide si 1 a un problème.
 
### Justification choix/ on a choisit de faire avec ce service car il est simple à mettre en place et qu'il permet de faire fonctionner le cluster natif. Ce service est là que parce qu'on a décidé de faire un cluster de base de donnée.


### Exposition réseau et sécurité/ on a besoin d'ouvrir seulement les ports lié au sql donc 6033 etc. vers les serveurs de base de données mais aussi ne provenance des serveurs web pour effectuer des requête sql. Ce service se trouve dans le réseau DATA donc au même endroit que les serveurs de base de donnée en 172.16.30.0/24


## INSTALLATION 
https://proxysql.com/documentation/installing-proxysql/
#### depuis là et depuis le github https://github.com/sysown/proxysql/releases/

### on installe avec wget et on rajoute la clé
`wget -O - 'https://repo.proxysql.com/ProxySQL/proxysql-3.0.x/repo_pub_key' | apt-key add -`

### après tout ça on peut faire la basique :
`sudo apt update`
`sudo apt install proxysql`


`mysq -u admin -p -h 127.0.0.1 _P 6032`

## SUR VM server SQL

### on créer un user qui a tous les accès depuis le proxysql
```
CREATE USER 'user'@'%' IDENTIFIED BY 'projetnuez2026';
GRANT ALL PRIVILEGES ON *.* TO 'user'@'172.16.30.54' WITH GRANT OPTION;
FLUSH PRIVILEGES;

```


## SUR VM PROXYSQL
#### MASTER
`INSERT INTO mysql_servers (hostgroup_id, hostname, port, max_connections)`
`VALUES (0, '172.16.30.51', 3306, 200);`

#### SLAVES
`INSERT INTO mysql_servers (hostgroup_id, hostname, port, max_connections)`
`VALUES (1, '172.16.30.52', 3306, 200);`

`INSERT INTO mysql_servers (hostgroup_id, hostname, port, max_connections)`
`VALUES (1, '172.16.30.53', 3306, 200);`

```
INSERT INTO mysql_users (usersername, password, default_hostgroup)
VALUES ('user', 'projetnuez2026', 0);

LOAD MYSQL USERS TO RUNTIME;
SAVE MYSQL USERS TO DISK;

```

### ET pour tester la connexion avec les nœuds de galera :

`SELECT hostgroup, srv_host, srv_port, ConnUsed, ConnOK, ConnERR FROM stats_mysql_connection_pool;`

#### ET on aura une sortie comme ça

- Tu as **3 serveurs MySQL** dans ProxySQL :

| hostgroup | srv_host     | srv_port | ConnUsed | ConnOK | ConnERR |
| --------- | ------------ | -------- | -------- | ------ | ------- |
| 0         | 172.16.30.51 | 3306     | 0        | 1      | 0       |
| 1         | 172.16.30.52 | 3306     | 0        | 1      | 0       |
| 1         | 172.16.30.53 | 3306     | 0        | 1      | 0       |
ConnOK = tout est bon la connexion a été établie.