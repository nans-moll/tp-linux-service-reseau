
#  Installer Nginx

Apres s'être connecté à la VM, on va installer Nginx :

`apt update` `apt install nginx`

Vérifie que Nginx tourne : 

`systemctl status nginx
`
Tu dois voir **active (running)**
Depuis **ta machine hôte**, ouvre un navigateur : 

`http://IP_DE_LA_VM` 

Tu dois voir : 
**Welcome to nginx!** 

 Voilà, le Serveur Web est créer, tu a plus qu'à créer ton site Web.