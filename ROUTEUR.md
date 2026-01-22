Pourquoi un routeur ?

Nous avons mis un routeur a dispositions un routeur sur notre serveur avant tout pour la sécurité de notre infrastructure  et ainsi éviter d'avoir tout sur un seul et même réseau pour la configuration de celui ci j'ai décider d'utiliser opnsense étant donner qu'il est souvent mis a jour il est plus stable et regorge de fonctionnalité.


Nous allons maintenant passer a l'installation et la configuration du routeur pour cela j'ai utiliser proxmox comme hyperviseur ayant a disposition un serveur a la maison

pour l'installation nous allons nous rendre sur le site de opnsense pour y installer l'iso et directement lancer une machine virtuelle sur debian.
https://opnsense.org/download/

voici le lien pour télécharger l'iso 

![[Pasted image 20260122124438.png]]

installation image type dvd pour ensuite la mettre directement sur proxmox 

![[Pasted image 20260122124722.png]]

une fois l'iso ajouter nous pouvons créer une vm en implémentant l'iso et donc ainsi passer a l'installation d'opnsense

pour l'installation d'opnsense c'est très simple il faut seulement entrer l'user : ``installer`` et mdp: ``opnsense`` (mot de passe que nous pourrons modifier plus tard dans l'installation)


![[Pasted image 20260122125255.png]]


une fois connecter nous atterrissons dans la zone d'installation la premiere etape consiste a choisir la langue dans mon cas j'ai choisis francais (langue du clavier)

![[Pasted image 20260122125546.png]]

pour la deuxième étape on nous demande le type d'installation nous allons sélectionner ZFS puis continuer 

![[Pasted image 20260122125736.png]]

puis a l'étape suivante nous allons sélectionner stripe car nous avons qu'un seul disque 

![[Pasted image 20260122125911.png]]

a la prochaine étape on nous demande de selectionner le disque nous avons qu'un seul disque a seletionner donc simplement appuyer sur continuer 

![[Pasted image 20260122130024.png]]

une fois l'installation terminer on nous propose de changer le mot de passe root c'est ce que j'ai fais et c'est conseiller pour la securité

![[Pasted image 20260122130130.png]]

ensuite via proxmox il faut ajouter toute les carte réseaux et les assigner pour chaque réseau different dans mon cas

vmbr0 = WAN
vmbr1 = DMZ
vmbr2 = WEB
vmbr3 = DATA
vmbr4 = ADMIN
 pour créer les cartes réseau nous allons nous rendre sur proxmox dans l'onglet

en cliquant sur l'onglet du profil et en nous dirigeant sur l'onglet network nous pouvons accéder a l'interface et créer nos carte réseaux

![[Pasted image 20260122131620.png]]

toutefois avant de lancer ne pas oublier de retirer l'iso opnsense pour ne pas que ca boot sur l'installation de ce dernier 

(pour retirer l'iso se rendre dans l'onglet hardware de la machine au pasage voici la configuration de ma vm)

![[Pasted image 20260122132127.png]]


une fois les carte créer nous pouvons nous rendre sur opnsense et ainsi assigner nos interfaces en cliquant ``1``  

![[Pasted image 20260122132250.png]]

et ensuite assigner chaque interface comme indiquer précédemment une fois configurer voici ce que ca donne.

![[Pasted image 20260122132400.png]]

ensuite pour nous allons assigner une addresse ip pour chaque réseau en cliquant sur`` 2 `` et ainsi configurer les adresses IP , les masques de sous réseaux et les range 

![[Pasted image 20260122132802.png]]

une fois ici il faut renter la carte que nous voulons configurer lui assigner un Gateway et ensuite rentrer la range pour les adresse IP que nous allons attribuer 

une fois tout fais voila ce que ca donne chaque machine est configurer nous pouvons desorm

![[Pasted image 20260122133005.png]]
