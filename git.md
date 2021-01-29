# GIT Cheat Sheet

## Commandes courantes

Commande | Commentaire
--- | --- 
`git add *`|Stage tous les fichiers modifiés (les ajoute à l'index)
`git checkout -- path/to/file/to/revert`|Annule les modifications d'un fichier not staged (le fichier est extrait depuis l'index donc les modifications non staged sont écrasées) "--" facultatif
`git checkout 9cfd4e43`|Checkout le commit dont l'id est 9cfd4e43. Le repo local se retrouve avec la tête détachée, utiliser 'git switch -' pour rattacher la tête
`git checkout tags/v1.3.0`|Checkout le tag dont le nom est v1.3.0 dans la `branche en cours. Ajouter -b pour créer une branche
`git cherry-pick 6c8f33b3`|Récupère le commit d'id 6c8f33b3 (il doit `obligatoirement être dans une autre branche)
`git cherry-pick my-branch~0 my-branch~1`|Applique les deux derniers commits de la branche my-branch à la branche en cours
`git clone --depth 1 <git_repo>`|Clone un repo avec une profondeur de 1, c’est-à-dire qu'on ne récupère que le dernier commit
`git commit --amend --date="$(date)"`|Change la date du dernier commit
`git commit -m "message"`|Commit les modifications actuellement sur le stage
`git config --global core.editor "code --wait"`|Utiliser VSCode comme éditeur par défaut à la place de VI
`git config --global pull.rebase true`|Indique à GIT de toujours faire un rebase `lors du pull
`git config --local core.autocrlf false`|Empêche GIT de remplacer les CRLF par des LF lors de la publication, très utile quand on publie des fichiers signés !
`git config --local credential.helper manager`|Indique à GIT de stocker les credentials dans Windows, ainsi il pose la question une seule fois
`git diff`|Voir les modifications pas encore commit
`git diff commit1 commit2`|Compare deux commits (ex HEAD~0, HEAD~1, 89de516, …)
`git diff nomfichier`|Affiche les modifications apportées à un fichier en particulier. Ajouter -b pour ignorer les fins de lignes
`git fetch <remote_name>`|Fetch les modifications d'un remote
`git log --graph --oneline`|Affiche une vue synthétique des derniers commits avec représentation graphique des branches
`$ git log --numstat --format="" b0d6e5b.. \| awk '{files += 1}{ins += $1}{del += $2} END{print "total: "files" files, "ins" insertions(+) "del" deletions(-)"}'`|Compte le nombre total d'insertions et de suppressions depuis un commit donné (b0d6e5b dans l'exemple)
`git pull remote_name master`|Pull les modifications d'un remote
`git push --all`|Push toutes les branches
`git push --delete origin tagname`|Supprime un tag sur le remote (git tag -d tagname pour supprimer le local)
`git push remote_name master`|Push les modifications vers un remote
`git push --set-upstream origin new-logo`|Push la branche actuelle qui n'existe `pas encore sur le remote (ou -u origin)
`git rebase -i 89de516`|Effectue un rebase interractif sur le commit 89de516
`git rebase --onto master`|Rebase la branche actuelle à partir de la master
`git remote`|Obtenir la liste des remotes
`git remote add remote_name https://github.com/remote_name/repo_name.git`|Ajouter un remote
`git remote prune origin`|Supprime les branches "remotes" du repo local qui n'existent plus sur le remote 
`git remote remove upstream`|Retirer un remote
`git reset file.cs`|Unstage le fichier file.cs
`git reset --hard`|Annule et supprime complètement les modifications staged
`git reset --soft HEAD~1`|Annule le dernier commit (les modifications reviennent `non staged)
`git rm NeedABreak/publish/needabreak-v1.0.0.zip`|Supprime un fichier. Si le `fichier existe localement on peut le conserver avec "--cached" ou le supprimer complètement avec "-f"
`git show 89de516`|Affiche le contenu d'un commit
`git stash`|Mets de côté toutes les modifications
`git stash apply`|Applique les modifications mises de côté
`git status`|Voir les fichiers pas encore commit
`git switch -`|Permet de rattacher la tête à un repo local auquel on l'avait détaché
`git switch -c new_branch_name`|Permet de créer une nouvelle branche à partir d'un repo local avec la tête détachée
`git whatchanged`|Affiche l'historique des commits
`set LESSCHARSET=UTF-8 (cmd) ou $env:LESSCHARSET="UTF-8" (powershell) ou LESSCHARSET=UTF-8 (bash)`|Défini l'encodage utilisé par less afin que les accents ne sautent plus. Définir la variable au niveau système pour être tranquille
`git fetch origin && git reset --hard origin/master && git clean -f -d`|Force l'obtention des commits du remote quand le repo local a divergé. Attention les commits locaux seront perdus

## Extras

### Erreur "Authentication failed"

En cas d'erreur "Authentication failed" : Ouvrir le credential manager (gestionnaire d'identification) et supprimer les comptes GIT enregistrés dans "informations d'identification Windows"

### Ajouter le bash GIT dans Windows Terminal

Ouvrir le fichier de configuration de Windows Terminal (settings.json) et ajouter cette section à la liste des profils :

```json
{
    "guid": "{d2a4c853-0b71-40e0-ac5e-d54338ce6529}",
    "hidden": false,
    "name": "Bash",
    "commandline": "C:\\Program Files\\Git\\bin\\bash.exe",
    "startingDirectory": "%HOMEPATH%\\source\\repos",
    "icon": "c:\\Icon\\Terminal.ico"
}
```

### Exécuter des commandes au démarrage du bash

Se placer dans le dossier "home" et créer un fichier .bashrc contenant les commandes à exécuter. Exemple :

```shell
cd
echo alias ll=\'ls -hal\' >> .bashrc
```
