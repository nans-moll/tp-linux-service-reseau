

#  Installer `Step-ca`

Pour utiliser les certificat de step-ca, il faut d'abord créer une nouvelle VM dédié a step-ca.
Une fois la VM créé, on ouvre un terminal dans lequel on va taper:

`apt-get update && apt-get install -y --no-install-recommends curl gpg ca-certificates`

`curl -fsSL https://packages.smallstep.com/keys/apt/repo-signing-key.gpg -o /etc/apt/keyrings/smallstep.asc`

`cat << EOF > /etc/apt/sources.list.d/smallstep.sources`
`Types: deb`
`URIs: https://packages.smallstep.com/stable/debian`
`Suites: debs`
`Components: main`
`Signed-By: /etc/apt/keyrings/smallstep.asc`
`EOF`

`apt-get update && apt-get -y install step-cli step-ca`

Step-ca et maintenant installer

#  Créer un certificat HTTPS

Pour créer un certificat, il faut faire :

`step ca init`

on a le choix entre plusieurs option on va prendre `Standelone` qui nous permet de tout gérer nous même.
On rentre ensuite le nom de domaine par lequel mes serveurs web seront joints.
On rentre également l'adresse IP et le PORT sur lequel mon serveur CA va écouter.
Vu que c'est un réseau interne on met :

`0.0.0.0:443`

- `0.0.0.0` → écoute sur **toutes les interfaces**
    
- `443` → port HTTPS standard


On choisi un nom pour le provisioner on va mettre `admin`.

Voici ce a quoi cela ressemble dans la console :
![[Pasted image 20260122143725.png]]




# Démarrer et vérifier `Step-ca`

Pour vérifier si `step-ca` est bien démarré on va faire 

`systemctl status step-ca`

si ce n'est pas actif :

`systemctl enable --now step-ca`

Puis on vérifie que ca écoute bien :

`ss -tlnp | grep 443`


# Problème rencontrer

lorsque j'ai fais `systemctl status step-ca` , la console me retourne l'erreur suivante :

*`step-ca.service could not be find`*

il faut donc créer nous même le service `systemd`.

`which step-ca` nous permet de vérifié ou ce trouve `step-ca`,
normalement le terminal nous retourne `/usr/bin/step-ca`.

pour créer le service in faut faire :

`nano /etc/systemd/system/step-ca.service`

et écrire dedans, sauf que j'ai essayé different code a l'interieur, aucun ne marché.

Comme par exemple celui si :

`[Unit]`
`Description=Smallstep Certificate Authority`
`After=network.target`

`[Service]`
`Type=simple`
`User=root`
`ExecStart=/usr/bin/step-ca /root/.step/config/ca.json`
`Restart=on-failure`
`LimitNOFILE=65536`

`[Install]`
`WantedBy=multi-user.target`

Lorsque je le rentre et que je sauvegarde, quand je fais `systemctl start step-ca` , j'obtiens toujours ces erreurs la :
![[Pasted image 20260122144822.png]]