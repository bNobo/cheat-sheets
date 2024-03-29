# Linux Cheat Sheet

## Commandes

Commande | Description
--- | ---
`alias ll='ls -lh'` | crée ou modifie un alias de commande
`passwd` | changer le mot de passe de l'utilisateur actuel (nécessite de connaitre le mot de passe)
`passwd <username>` | changer le mot de passe de l'utilisateur username (ne nécessite pas de connaitre son mot de passe)
`cat /etc/passwd` | afficher la liste des utilisateurs
`useradd a.bob` | crée un nouvel utilisateur a.bob
`usermod -a -G root a.bob` | ajouter l'utilisateur a.bob au groupe root
`rm -rf folder_name` | supprime le répertoire folder_name et tout son contenu de manière récursive. **Il n'y a aucune demande de confirmation**
`false` | échoue en ne faisant rien, les arguments sont ignorés
`apt update` | met à jour les packages
`apt upgrade` | promeut les packages
`crontab -e` | ouvre l'éditeur des tâches cron (planificateur de jobs)
`less input` | affiche le contenu de l'entrée page par page
`tail` | affiche la fin d'un fichier
`curl wttr.in/Montpellier` | affiche la météo de Montpellier
`telnet towel.blinkenlights.nl` | Star Wars épisode IV, en ASCII-Art ^^
`df -h` | Affiche l'espace disque restant dans un format lisible par un humain
`du -h` | Affiche l'espace disque utilisé par chaque répertoire
`pwd` | Affiche le chemin complet du répertoire actuel
`grep -H --color 'text to find' <file_pattern>` | Recherche un texte dans tous les fichiers correspondant au pattern (ex : \*.html). Affiche toutes les lignes contenant le texte recherché précédées du nom du fichier (-H). --color permet de coloriser le texte recherché pour le rendre plus visible.
`htop` | Affiche les threads avec utilisation CPU et mémoire
`sudo -s` | Execute le shell en tant que root, ainsi plus besoin de taper "sudo" à chaque commande
`strings ./somenetcore.dll \| egrep '^[0-9]+\.[0-9]+\.[0-9]+$'` | Affiche le numéro de version d'assembly d'une dll net core (SemVer)
`ps axo pid,ppid,pgrp,tty,tpgid,sess,comm \|awk '$2==1' \|awk '$1==$3'` | Liste les daemons
`cat /etc/os-release` | Affiche la version de l'OS
`sudo service cron status` | Affiche le statut d'exécution de cron
`sudo service cron start` | Démarre le service cron
`sudo visudo` | Edite le fichier des sudoers

## /etc/hosts

`192.168.1.1 mon.domaine.fr  alias`

## /etc/resolv.conf

Paramétrer l'IP du serveur DNS :

`nameserver 192.168.58.41`

## /etc/sudoers

> Ne pas éditer directement ce fichier mais utiliser la commande `sudo visudo`

```
# permet à tous les sudoers d'exécuter la commande `service cron start` sans avoir à taper de mot de passe
%sudo ALL=NOPASSWD: /usr/sbin/service cron start
```

## /etc/ssh/sshd_config

Ce fichier permet de configurer le daemon SSH. Par exemple le port à utiliser (22 par défaut) ou activer l'authentification par mot de passe (désactivée par défaut pour des raisons de sécurité : prévention du brute force).

## systemctl

affiche le statut d'un service :

`systemctl status myservice`

Démarre, redémarre ou stoppe un service :

`sudo systemctl start|stop|reload myservice`

Après modification d'un fichier *.service* il faut redémarrer le daemon pour le recharger :

`sudo systemctl daemon-reload`

## Activer la connexion SSH sans mot de passe

```bash
# générer une paire de clés RSA
ssh-keygen -t rsa -f <keyname>
# copier la clé publique sur la machine distante (on peut aussi la copier manuellement dans le fichier ~/.ssh/authorized_keys)
ssh-copy-id -i ~/.ssh/<keyname>.pub <login>@<remote_address>
# se connecter sans mot de passe
ssh -i ~/.ssh/<keyname> <login>@<remote_address>
```

## Mettre à jour les sources de packages

Les serveurs de noms utilisés se trouvent dans `/etc/resolv.conf`

La liste des sources de package se trouve dans `/etc/apt/sources.list`

Lorsqu'on ajoute une source il faut également ajouter sa clef publique dans `/etc/apt/trusted.gpg.d/` afin qu'aptitude puisse vérifier la signatures des packages.

> Astuce : quand on utilise 2 distributions différentes sous WSL, on peut facilement recopier les clefs publiques de l'une à l'autre en utilisant un serveur HTTP. Dans le répertoire des clefs à récupérer taper `python3 -m http.server`. Dans l'autre distro, se placer dans le répertoire des clefs et taper `wget <ip>:8000/<key_name.gpg>`.

## journalctl

Afficher le journal d'une unité donnée :

```bash
journalctl -u <servicename>
```
