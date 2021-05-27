# Bash cheat sheet

Commande | Description
--- | ---
`export HTTP_ECHO_PORT=1322 && node index.js` | set une variable d'environnement avant de démarrer une appli node en une seule ligne

## Astuce

Le back tick permet d'exécuter une commande autant de fois que de lignes retournées par la commande. Par exemple :

```bash
docker rmi -f `docker images | grep previewservice.azurecr.io/previewapi | awk '{print $3}'`
```

Ici la commande `docker rmi -f` sera exécutée autant de fois que de lignes retournées par la commande `docker images`

Autre exemple, ici pour lister l'espace disque occupé par chaque répertoire racine :

```bash
sudo du -sh `ls -ld /* | awk '{print $9}'`
```
