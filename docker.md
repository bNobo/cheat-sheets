# Docker Cheat Sheet

Commande | Description
--- | ---
`docker run -p 1664:80 monrepo/http-echo` | Démarre un container avec l'image monrepo/http-echo et bind le port 1664 local sur le port 80 du container (port sur lequel l'application http-echo écoute par défaut). L'image est téléchargée et installée si pas présente sur le poste. On peut ensuite tester l'appli via l'URL http://localhost:1664
`docker exec -i -t 80f6a4603277 bash` | Exécute un bash interactif dans un container existant dont l'ID est 80f6a4603277
`docker run -i -t --entrypoint bash image:tag` | Idem ci-dessus mais en remplacant l'entry point de l'image par la commande bash
`docker network create papinet` | Crée un network de type bridge et nommé papinet
`docker run -d -p 27017:27017 --name mongoserver --network papinet mongo:bionic` | Démarre un container en le rattachant à un network. Tous les containers sur le même network peuvent communiquer entre eux, dans cet exemple un autre container pourrait accéder à celui-ci via `mongodb://mongoserver:27017`. Ca fonctionne pour tous les protocoles, ex `http://<containername>:<port>`
`docker commit --squash sqlserver myregistry.io/sqlserver/myimage:1.0.0` | Ma commande préférée :) Permet de créer une nouvelle image à partir d'un container existant. Ne pas oublier le `--squash` sinon l'image gonfle à chaque commit.

## Suppression d'images en masse

```bash
docker rmi -f `docker images | grep <repository_name> | awk '{print $3}'`
```

Supprime toutes les images d'un repository donné. A noter l'utilisation du back tick qui permet d'exécuter la commande `docker rmi` avec comme argument chaque ligne retournée par la commande `docker images`

Et pour supprimer tous les tags associés à une image et finalement supprimer l'image :

```bash
docker rmi `docker images | grep <image_id> | awk '{printf "%s:%s\n", $1, $2}'`
```

## En cas d'erreur lors du binding d'un port qui n'est pourtant pas utilisé

Ca m'est arrivé avec le port 1433 de SQL Server mais à priori le problème peut se produire avec n'importe quel port. Il semble que hyper-v réserve une plage de ports. Ces derniers deviennent inutilisables même s'il ne sont pas effectivement utilisés. Premièrement il faut déjà vérifier que le port n'est pas tout simplement vraiment utilisé :

```bash
netstat -aon
```

S'il apparait dans la liste alors il faut stopper l'application. L'id du process apparait en dernière colonne. Il suffit de faire un `kill`.

Si le port en question n'est pas dans la liste alors cette commande permet de lister les plages d'exclusion de ports : 

```bash
netsh interface ipv4 show excludedportrange protocol=tcp
```

Si le port désiré est inclu dans une des plages réservées alors, souvent celà vient d'hyper-v. Pour le résoudre (dans une invite avec droits admin) : 

1. Disable hyper-v (which will required a couple of restarts)

```bash
dism.exe /Online /Disable-Feature:Microsoft-Hyper-V
```

2. When you finish all the required restarts, reserve the port you want so hyper-v doesn't reserve it back

```bash
netsh int ipv4 add excludedportrange protocol=tcp startport=1433 numberofports=2
```

3. (facultatif, perso je n'utilise pas hyper-v) Re-Enable hyper-V (which will require a couple of restart)

```bash
dism.exe /Online /Enable-Feature:Microsoft-Hyper-V /All
```

Si besoin de supprimer une plage de ports réservée :

```bash
netsh interface ipv4 delete excludedportrange protocol=tcp 1433 2
```

Source : https://github.com/docker/for-win/issues/3171

## Debugger un Dockerfile

A chaque étape, docker crée une image intermédiaire et affiche son ID.

```
[1/2] STEP 11/12: WORKDIR "/src/Merlin.UnitTests"
--> e83032950bdb
```

A moins d'utiliser l'argument `--no-cache` ces images sont conservées et on peut donc s'en servir pour démarrer un container.

```bash
$ docker run -it --rm e83032950bdb bash
```

On peut ainsi ouvrir un shell et explorer le container dans l'état où il se trouve quand l'erreur se produit. Par exemple s'il s'agit d'un problème de chargement de dépendances d'une librarie native on peut exécuter la commande `ldd` afin d'identifier les dépendances manquantes.

```bash
ldd libcvextern.so
        linux-vdso.so.1 (0x00007ffca4fd2000)
        libgeotiff.so.5 => not found
        libopenjp2.so.7 => not found
        libdc1394.so.25 => not found
[...]
```
