
# BASTIEN

#BASTIEN
# Slide 1 - Présentation équipe +projet de base

# Slide 2 - Présentation projet 
## Entreprise qui nous contacte pour faire une infra complète autour de leur site web / essayer de respecter cahier des charges 

#NANS
# Slide 3 - NANS PROXMOX


#NANSETBASTIEN
# Slide 4 - pré schéma réseau 

![[Pasted image 20260123103252.png]]


#NANS
# Slide 5 - NANS OPSENSE
## pres son rôle justifier sa présence où il est et comment il est sécurisé 



#LILIAN
# Slide 6 - LILIAN PRES SITE


#BASTIEN
# Slide 7 - Serveur web avec nginx 
## pres son rôle justifier sa présence où il est et comment il est sécurisé 
#### -> hébergement + présence 3 servers pour cluster
#### nginx > apache2 et comme loadbalancer nginx go tout faire ne nginx
##### -> plus stable et consomme moins en mémoire 



#EDDY
# Slide 8 - EDDY CERTIF WEB
## pres son rôle justifier sa présence où il est et comment il est sécurisé 



#BASTIEN
# Slide 9 - LOADBALANCER NGINX
## pres son rôle justifier sa présence où il est et comment il est sécurisé 
### différente façon de répartir la charge

![[{AAE07279-5C36-4996-A113-C246DC382A33}.png]]

#ETIENNE
# Slide 10 - POWERDNS-ADMIN
## pres son rôle justifier sa présence où il est et comment il est sécurisé 

Role du service :
1/ a quoi sert-il 
2/ est t'il critique







Justification du choix 
1/pourquoi ce service 
2/alternative possible ?




#NANS 

# Slide 11 - BASTION GOTELEPORT
## pres son rôle justifier sa présence où il est et comment il est sécurisé 

# Slide 12 - OBSERVABILITE GRAFANA
## pres son rôle justifier sa présence où il est et comment il est sécurisé 



#BASTIEN
# Slide 13 - CLUSTER-BDD GALERA
## pres son rôle justifier sa présence où il est et comment il est sécurisé 
### cluster bdd = continuité de service bdd comme cluster web mais natif avec galera
### inclus a mariadb donc compatible et facile a mettre en place
#### Sous réseau DATA
# Slide 14 - PROXYSQL
## pres son rôle justifier sa présence où il est et comment il est sécurisé 
### load balancer de bdd tout simplement 
### pk proxysql ? psq dimitri il me l'a dit j'ai tester ça a marché dcp j'ai pas cherché mieux
#### Sous réseau DATA

#NANS
# Slide 15 - BACKUP
## pres son rôle justifier sa présence où il est et comment il est sécurisé 




# DEMO - infra