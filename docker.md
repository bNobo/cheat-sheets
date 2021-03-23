# Docker Cheat Sheet

Commande | Description
--- | ---
`docker run -p 1664:80 secib/http-echo` | Démarre un container avec l'image secib/http-echo et bind le port 1664 local sur le port 80 du container (port sur lequel l'application http-echo écoute par défaut). L'image est téléchargée et installée si pas présente sur le poste. On peut ensuite tester l'appli via l'URL http://localhost:1664
`docker exec -i -t 80f6a4603277 bash` | Exécute un bash interactif dans un container existant dont l'ID est 80f6a4603277
`docker run -i -t --entrypoint bash image:tag` | Idem ci-dessus mais en remplacant l'entry point de l'image par la commande bash
`docker network create papinet` | Crée un network de type bridge et nommé papinet
`docker run -d -p 27017:27017 --name mongoserver --network papinet mongo:bionic` | Démarre un container en le rattachant à un network. Tous les containers sur le même network peuvent communiquer entre eux, dans cet exemple un autre container pourrait accéder à celui-ci via `mongodb://mongoserver:27017`. Ca fonctionne pour tous les protocoles, ex `http://<containername>:<port>`

## bonus

```
docker rmi -f `docker images | grep <repository_name> | awk '{print $3}'`
```

Supprime toutes les images d'un repository donné. A noter l'utilisation du back tick qui permet d'exécuter la commande `docker rmi` avec comme argument chaque ligne retournée par la commande `docker images`
