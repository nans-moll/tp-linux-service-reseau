pour la backup l'ideal que j'ai trouver et je pense le plus simple pour moi c'est d'installer directement proxmox backup server

pour installer backup server nous devons nous rendre directement sur le site officiel proxmox 

https://www.proxmox.com/en/downloads

ensuite copier le lien de téléchargements de backup server pour l'inserer a cette endroit precis sur proxmox

![[Capture d’écran 2026-01-20 100346.png]]
puis cliquer sur download form url et inscrire l'url que nous avons copier précédemment 

![[Capture d’écran 2026-01-22 144733.png]]

une fois fais notre iso de backup est enfin importer nous pouvons maintenant installer une vm avec backup server mais avant ca j'ai retrouver 2 disque dur qui trainais je vais donc faire un raid 1 avec (mirroir) pour ca nous allons nous rendre dans l'onglet `ZFS`  pour y effectuer un mirroir avec nos deux disque dur 

![[Pasted image 20260122152809.png]]

une fois sur l'interface sélectionnez le disque puis dans raid level : Mirror puis appuyez sur create dans mon cas ca n'a pas marcher 
j'ai eu cette erreur 


![[015f393a-56c6-4dca-9412-c41909adf3b5.png]]
car il restait des données dans mes disques et probablement car les disques de 1to n'était pas de la même marque et donc ne compterais pas le même stockage je suis donc passer dans le terminal et est effectuer ses deux commande l'une pour forcer proxmox a vider mes deux disques 


``wipefs -a /dev/sdb 
``wipefs -a /dev/sdc

une fois fais ca n' a toujours pas marcher Ducoup je suis passer a une autre méthode et j'ai forcer la création du pool que j'ai appeler backup pool avec cette commande 

![[Capture d’écran 2026-01-22 151228.png]]

maintenant je peux faire ma Vms correctement pour accueillir backup server petite capture d'ecran pour montrer que tout a bien marcher

![[Pasted image 20260122153200.png]]

-------------------------------------------------------------------------

installation de Backup server


