# Docker Cheat Sheet

Commande | Description
--- | ---
`docker run -p 1664:80 secib/http-echo` | Démarre un container avec l'image secib/http-echo et bind le port 1664 local sur le port 80 du container (port sur lequel l'application http-echo écoute par défaut). L'image est téléchargée et installée si pas présente sur le poste. On peut ensuite tester l'appli via l'URL http://localhost:1664
`docker exec -i -t 80f6a4603277 bash` | Exécute un bash interactif dans un container existant dont l'ID est 80f6a4603277
