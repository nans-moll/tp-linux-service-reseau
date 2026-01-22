
## Les serveurs web sont là pour héberger le site web 
#### Pourquoi 3 ? Cluster non-natif avec le proxy/loadbalancer 


### le rôle de ce service est d'héberger le site web de gestion de ticket.
 
### Justification choix/ on a choisit de faire avec Nginx  > facile à installer > fiable  | pareil on aurait pu choisir apache2 mais on a choisis nginx comme ça aussi c'était cohérent avec le proxy, tout sur nginx.


### Exposition réseau et sécurité/ on a besoin d'ouvrir seulement les ports 80 si http et 443 si https et à la limite 22 pour ssh mais que pour notre réseau de vm admin. cette machine se trouve dans le sous réseau 10.10.20.0/24 = sous réseau "WEB"


# INSTALLATION

## Pour installer ce service, rien de plus simple 
`sudo apt update`
`sudo apt install nginx`
`systemctl start nginx`

### après ça c'est déjà prêt on a plus qu'à mettre les fichiers du site web
#### Comme il est en html/css/js on va devoir rajouter quelques petits truc comme :

`sudo apt install nodejs`
pour pouvoir lancer le index.js

`sudo apt install npm`
pour installer les packages du projet avec

`npm install <NomduPackage>`
et on avait comme package :
* express
* socket.io
* multer
* cookie-parser
* mysql

### Il ne reste plus qu'à lancer le site avec `node /var/www/html/index.js`


