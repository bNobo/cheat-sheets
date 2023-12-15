# Bash cheat sheet

Commande | Description
--- | ---
`export HTTP_ECHO_PORT=1322 && node index.js` | set une variable d'environnement avant de démarrer une appli node en une seule ligne
`printenv` | liste les variables d'environnement
`command \|\| command` | exécute la seconde commande uniquement si la première échoue
`for i in 1 2 3 4; do echo $i; done` | boucle for
`for i in {1..17}; do echo $1; done` | boucle for sur un range
CTRL+Z | envoi le process en arrière plan
`fg` | ramène le process au premier plan
`history [n]` | affiche l'historique des dernières commandes
`!!` | rappele la dernière commande
`!502` | rappele la commande #502 dans l'historique
`!command` | rappele la commande "command" avec les mêmes arguments que la dernière fois qu'elle a été appelée
`echo !$` | !$ contient le dernier argument de la dernière commande exécutée
`echo "coucou" \| xargs echo` | xargs permet de convertir la sortie de la commande précédente en argument pour la commande suivante
`echo ${string_var:(-2)}` | affiche les deux derniers caractères de la variable string_var

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

### Back tick

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

### Créer un checksum (hash) et le convertir en base64

La commande `sha256sum` permet de générer un hash à partir du contenu d'un fichier mais le résultat est sous forme de hexstring alors que le navigateur attend du base64. La commande ci-dessous permet de convertir le hexstring en binaire avant d'envoyer les données à la commande base64 et ainsi obtenir directement un checksum utilisable dans le navigateur.

```bash
$ sha256sum --text script.js | xxd -r -p | base64
2wi3v50GQUHK7XnLYfYCoUIWxObbOC7qbU3cptMBBb8=
```

Il est également possible d'encoder directement du texte sans passer par un fichier :

```bash
$ printf 'coucou' | sha256sum --text | xxd -r -p | base64
O2TRH/CsXaaiYrNJd7s9Ka4KTAMJR8EeGg2eUchI93I=
```

Eviter d'utiliser la commande `echo` ou `nano` car ces derniers ajoutent un `\n` à la fin.

Attention, si la chaîne à encoder contient un caractère $, alors il faut l'échapper ou bien utiliser une simple cote afin qu'il ne soit pas interprété comme une variable.

> Pour faire un SHA512 utiliser la commande `sha512sum`. Pour choisir un autre algorithme utiliser la commande `shasum -a`.

Pour l'utiliser dans l'attribut `integrity` de l'élément `<script>` il faut ajouter le préfixe `sha-256`. Pour le faire en une seule ligne :

```bash
$ printf "sha256-$(sha256sum --text script.js | xxd -r -p | base64)"
sha256-2wi3v50GQUHK7XnLYfYCoUIWxObbOC7qbU3cptMBBb8=
```

## Changer la locale

```bash
$ locale
LANG=en_US.UTF-8
LANGUAGE=
LC_CTYPE="en_US.UTF-8"
LC_NUMERIC="en_US.UTF-8"
LC_TIME="en_US.UTF-8"
LC_COLLATE="en_US.UTF-8"
LC_MONETARY="en_US.UTF-8"
LC_MESSAGES="en_US.UTF-8"
LC_PAPER="en_US.UTF-8"
LC_NAME="en_US.UTF-8"
LC_ADDRESS="en_US.UTF-8"
LC_TELEPHONE="en_US.UTF-8"
LC_MEASUREMENT="en_US.UTF-8"
LC_IDENTIFICATION="en_US.UTF-8"
LC_ALL=
```
Sélectionner la locale désirée :

```bash
$ locale -a
[...]
$ export LC_ALL="fr_FR"
```
