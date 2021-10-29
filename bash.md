# Bash cheat sheet

Commande | Description
--- | ---
`export HTTP_ECHO_PORT=1322 && node index.js` | set une variable d'environnement avant de démarrer une appli node en une seule ligne
`printenv` | liste les variables d'environnement
`command \|\| command` | exécute la seconde commande uniquement si la première échoue
`for i in 1 2 3 4; do echo $i; done` | boucle for
CTRL+Z | envoi le process en arrière plan
`fg` | ramène le process au premier plan
`history [n]` | affiche l'historique des dernières commandes
`!!` | rappele la dernière commande
`!502` | rappele la commande #502 dans l'historique
`!command` | rappele la commande "command" avec les mêmes arguments que la dernière fois qu'elle a été appelée
`echo !$` | !$ contient le dernier argument de la dernière commande exécutée
`echo "coucou" \| xargs echo` | xargs permet de convertir la sortie de la commande précédente en argument pour la commande suivante

## Arguments

Tester un argument vide :

```bash
if [ -z "$1" ] 
then
  echo "empty arg"
fi
```

Tester l'existence d'un répertoire :

```bash
if [[ -d "$1" ]]
then
    echo "$1 already exists."
fi
```

Récupérer le code de sortie renvoyé par un script bash :

```bash
command   # execute some command
echo $?   # get exit code
```

## Astuces

Le back tick permet d'exécuter une commande autant de fois que de lignes retournées par la commande. Par exemple :

```bash
docker rmi -f `docker images | grep previewservice.azurecr.io/previewapi | awk '{print $3}'`
```

Equivalent avec `xargs`:

```bash
docker images | grep previewservice.azurecr.io/previewapi | awk '{print $3}' | xargs docker rmi -f
```

Ici la commande `docker rmi -f` sera exécutée autant de fois que de lignes retournées par la commande `docker images`

Autre exemple, ici pour lister l'espace disque occupé par chaque répertoire racine :

```bash
sudo du -sh `ls -ld /* | awk '{print $9}'`
```

Equivalent avec `xargs`:

```bash
ls -ld /* | awk '{print $9}' | xargs sudo du -sh
```
