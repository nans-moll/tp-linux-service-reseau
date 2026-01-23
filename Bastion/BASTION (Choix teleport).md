

commençons par créer une simple Machine virtuelle pour pouvoir accueillir Debian 12 je lui est mis 4Go de ram 

![[Pasted image 20260121144515.png]]

Une fois avoir créer ma machine virtuelle ainsi que mes utilisateurs nous pouvons passer a l'installation de téléport pour me faciliter la tache je me suis connecter en SSH depuis l'une de mes machines connecter sur le réseau admin  

en premier temps effectuer un Apt update et upgrade pour voir et faire les potentiels mise a jours (important meme si notre vm est toute fraiche):

![[Capture d’écran 2026-01-21 142551.png]]

ensuite ajoutons la clés gpg qui permet la configuration du gestionnaire de paquet et ainsi préparer l'installation de téléport 

![[Capture d’écran 2026-01-21 142503.png]]

ensuite passons a l'installation de teleport et la mise a jour des paquets a l'aide de cette commande 

``sudo apt update
``sudo apt-get install ${TELEPORT_PKG?}

ensuite nous allons effectuer une commande permettant de générer un fichier de configuration prêt a l'emploie que nous modifierons par la suite dans ``/etc/teleport.conf``  copier depuis ce site web [[#https://blog.stephane-robert.info/docs/securiser/acces/teleport/]]

``sudo teleport configure -o file --acme --acme-email=admin@stephrobert.tech --cluster-name=teleport.stephrobert.tech

une fois la configuration importer nous pouvons maintenant aller configurer le fichier dans /etc/teleport.conf

voici ma configuration de base j'ai modifier les noms pour acceder directement a l'interface de teleport via ma vm admin

![[Capture d’écran 2026-01-21 143257.png]]

une fois le fichier modiifer nous pouvons relancer le systeme

![[Capture d’écran 2026-01-21 143416.png]]

une fois le fichier modifier nous pouvons des a présent lancer téléport et voir ssi teleport est bien lancer a l'aide de ses deux commandes 

sudo 

![[Capture d’écran 2026-01-21 142223.png]]

 mais au début ca n'a pas marcher j'ai eu cette erreur 
 ![[Capture d’écran 2026-01-21 143105.png]]

en menant mes recherches sur internet j'ai pris la décision de désactiver la fonction acme (protocole permettant d'automatiser la délivrance des certificat ssl ) une fois mis sur "no"
en restart le système pour sauvegarder les modification du fichier  
j'ai pu accéder a l'interface de téléport

![[Capture d’écran 2026-01-21 143416.png]]

avant de pouvoir accéder a téléport nous devons créer un utilisateur a l'aide de cette de commande dans mon cas c'est l'admin 

`tctl users add admin --roles=editor,access --logins=outscale

	-----------------------------------------------------------------------------
Nous avons maintenant Accéder à l'interface ! 

![[Capture d’écran 2026-01-21 143642.png]]


ensuite nous pouvons accéder a l'interface pour ensuite créer notre compte admin 

![[Pasted image 20260121152630.png]]

ensuite nous pouvons lier notre A2F pour plus de sécurité dans mon cas j'ai utiliser l'application duo cisco

![[Capture d’écran 2026-01-21 152737.png]]

une fois avoir créer son compte nous pouvons des a présent procéder a l'enrôlement de nos autres serveurs pour pouvoir s'y connecter en ssh

![[Capture d’écran 2026-01-21 153849.png]]

une fois dans l'interface nous pouvons nous connecter a téléport moi dans mon cas ca ne marchais pas j'ai du creer un utilisateur appeler outscale sur ma machine teleport voici l'erreur que j'avais une fois le user ajouter j'ai pue me connecter en ssh

![[Capture d’écran 2026-01-21 154150.png]]

voici a quoi ca ressemble quand nous nous connectons

![[Capture d’écran 2026-01-21 155004.png]]
	une fois connecter je vais creer un user pour chaque vm et copier les liens qu'ils me donnent pour pouvoir afficher mes vm dans le bastion

