### le rôle de connecter les 3 serveurs de base de données comme si il n'était qu'on afin d'assurer une continuité de service satisfaisant. Ce service est important et très utile mais pas nécessairement obligatoire 
 
### Justification choix/ on a choisit de faire avec ce service car c'est inclus dans mariadb , simple à mettre en place.  


### Exposition réseau et sécurité/ on a pas besoin d'ouvrir de port pour les connecter entre elle tant qu'elle sont dans le même sous-réseau donc ici un sous-réseau réservé pour les serveurs SQL. Et ensuite accepter les requêtes depuis le ProxySQL. Elles se trouvent dans le réseau DATA en 172.16.30.0/24

## 1/LES PREREQUIS
### Avoir un nombre impaire de serveurs (ici 3) sur le même sous réseau 

- **SRV-SQL-1**
    - Adresse IP : 172.16.30.51/24
- **SRV-SQL-2**
    - Adresse IP : 172.16.30.52/24
- **SRV-SQL-3**
    - Adresse IP : 172.16.30.51/24

#### 2/Installation mariadb / galera

Sur les 3 machines :
`sudo apt-get update
`sudo apt-get install mariadb-server`

`
Ensuite on choisit 1 des 3 pour être celui sur lequel on aura galera

`sudo apt-get install galera-4
`ls /etc/mysql/mariadb.conf.d/60-galera.cnf`

### Et on rajoute ça dans la conf en mettant bien les bonnes ips

```
[galera]
# Mandatory settings
wsrep_on = ON
wsrep_provider = /usr/lib/galera/libgalera_smm.so
wsrep_cluster_name = "Galera_Cluster_IT-Connect"
wsrep_cluster_address = gcomm://192.168.1.6,192.168.1.25,192.168.1.196
binlog_format = row
default_storage_engine = InnoDB
innodb_autoinc_lock_mode = 2
innodb_force_primary_key = 1

# Allow server to accept connections on all interfaces.
bind-address = 0.0.0.0

# Optional settings
#wsrep_slave_threads = 1
#innodb_flush_log_at_trx_commit = 0
log_error = /var/log/mysql/error-galera.log
```

## 3/ On démarre le cluster et redémarre Mariadb

`sudo systemctl stop mariadb`
`sudo galera_new_cluster`

On se connecte à l'interface de mariadb

`mysql -u root -p`

et `show status like 'wsrep_cluster_size';` pour voir combien de noeud sont connecté et après avoir démarrer mariadb sur tout les serveur ça doit ressembler à ça :
![[{396095B5-3AC2-4485-A0B1-360436004C18}.png]]

et toc tout est bon.