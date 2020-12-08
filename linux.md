# Linux Cheat Sheet

Commande | Description
--- | ---
`alias ll='ls -lh'` | crée ou modifie un alias de commande
`passwd` | changer son mot de passe
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
