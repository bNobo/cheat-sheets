# GIT Cheat Sheet

## Commandes courantes

Commande | Commentaire
--- | --- 
`git add *`|Stage tous les fichiers modifiés (les ajoute à l'index)
`git branch -D branch && git checkout branch`|Méthode plus simple et pragmatique pour reset une simple branche locale qui a divergé
`git checkout origin/main -- path/to/file/to/revert`|Récupère uniquement le fichier path/to/file/to/revert depuis la branche origin/main
`git checkout 9cfd4e43`|Checkout le commit dont l'id est 9cfd4e43. Le repo local se retrouve avec la tête détachée, utiliser 'git switch -' pour rattacher la tête
`git checkout tags/v1.3.0`|Checkout le tag dont le nom est v1.3.0 dans la `branche en cours. Ajouter -b pour créer une branche
`git checkout -b main --track <remote>/main`|Quand plusieurs remotes il faut préciser le nom complet avec --track si une branche avec le même nom existe dans plusieurs
`git cherry-pick 6c8f33b3`|Récupère le commit d'id 6c8f33b3 (il doit `obligatoirement être dans une autre branche)
`git cherry-pick my-branch~0 my-branch~1`|Applique les deux derniers commits de la branche my-branch à la branche en cours
`git clean -fd`|Supprime les fichiers non suivis. Remplacer `f` par `n` pour dry run. Ajouter `x` pour supprimer également les fichiers exclus par `.gitignore` ce qui permet de remettre le repo dans le même état que le remote.
`git clone --depth 1 <git_repo>`|Clone un repo avec une profondeur de 1, c’est-à-dire qu'on ne récupère que le dernier commit
`git commit --amend --date="$(date)"`|Change la date du dernier commit
`git commit -m "message"`|Commit les modifications actuellement sur le stage
`git config --global core.editor "code --wait"`|Utiliser VSCode comme éditeur par défaut à la place de VI
`git config --global pull.rebase true`|Indique à GIT de toujours faire un rebase `lors du pull
`git config --local core.autocrlf false`|Empêche GIT de remplacer les CRLF par des LF lors de la publication, très utile quand on publie des fichiers signés !
`git config --local credential.helper manager`|Indique à GIT de stocker les credentials dans Windows, ainsi il pose la question une seule fois
`git config --global push.autoSetupRemote true`|Fait automatiquement le `--set-upstream` lors du premier `git push` d'une branche
`git count-objects -vH`|Affiche la taille du repo
`git describe --tags`|Affiche le dernier tag appliqué sur la branche
`git diff`|Voir les modifications pas encore commit
`git diff commit1 commit2`|Compare deux commits (ex HEAD\~0, HEAD\~1, 89de516, …)
`git diff nomfichier`|Affiche les modifications apportées à un fichier en particulier. **Ajouter -b pour ignorer les fins de lignes**
`git diff --stat 118f63c`|Affiche un résumé avec le nombre d'ajouts et suppressions effectués dans chaque fichier + total depuis le commit 118f63c
`git diff --stat main...topic`|Affiche les modifications apportées à la branche topic depuis le moment où elle a été tirée de la branche main`
`git diff --diff-filter=D --summary 'origin/main@{12 month ago}...origin/main'`|Liste tous les fichiers supprimés au cours des 12 derniers mois
`git fetch <remote_name>`|Fetch les modifications d'un remote
`git fetch && git remote prune origin && git branch -vv \| grep ': gone]'\|  grep -v "\*" \| awk '{ print $1; }' \| xargs -r git branch -D`|Supprime toutes les branches qui ont été push et qui n'existent plus sur le remote (gone).
`git fetch origin && git reset --hard origin/main && git clean -f -d`|Force l'obtention des commits du remote quand le repo local a divergé. Attention les commits locaux seront perdus
`git log --graph --oneline --all`|Affiche une vue synthétique des derniers commits avec représentation graphique des branches
`$ git log --numstat --format="" b0d6e5b.. \| awk '{files += 1}{ins += $1}{del += $2} END{print "total: "files" files, "ins" insertions(+) "del" deletions(-)"}'`|Compte le nombre total d'insertions et de suppressions depuis un commit donné (b0d6e5b dans l'exemple)
`git log --diff-filter=D --summary`|Affiche une liste de tous les commits qui ont supprimé des fichiers dans la branche actuelle
`git log -p -S 'Texte recherché' -- Dossier/projet.csproj`|Recherche un commit qui ajoute ou supprime le texte recherché dans le fichier projet.csproj
`git pull remote_name main`|Pull les modifications d'un remote. Si option pull.rebase=true alors GIT effectue automatiquement un rebase de la branche courante sur la branche main, ce qui permet de nettoyer les éventuels commits issus d'une branche intermédiaire.
`git push --all`|Push toutes les branches
`git push --delete origin tagname`|Supprime un tag sur le remote (git tag -d tagname pour supprimer le local)
`git push --set-upstream origin new-logo`|Push la branche actuelle qui n'existe `pas encore sur le remote (ou -u origin)
`git push origin v1.5`|Push un tag sur le remote
`git push origin --delete <tagname>`|Supprime un tag sur le remote
`git push origin --tags`|Push tous les tags sur le remote
`git push remote_name main`|Push les modifications vers un remote
`git rebase -i 89de516`|Effectue un rebase interractif sur le commit 89de516
`git rebase --onto main`|Rebase la branche actuelle à partir de la main
`git remote`|Obtenir la liste des remotes
`git remote add remote_name https://github.com/remote_name/repo_name.git`|Ajouter un remote
`git remote prune origin`|Supprime les branches "remotes" du repo local qui n'existent plus sur le remote 
`git remote remove upstream`|Retirer un remote
`git reset file.cs`|Unstage le fichier file.cs
`git reset --hard`|Annule et supprime complètement les modifications staged
`git reset --soft HEAD~1`|Annule le dernier commit (les modifications reviennent `non staged)
`git rm NeedABreak/publish/needabreak-v1.0.0.zip`|Supprime un fichier. Si le `fichier existe localement on peut le conserver avec "--cached" ou le supprimer complètement avec "-f"
`git show <commit_hash>`|Affiche le contenu d'un commit donné
`git show <commit_hash>:<chemin/du/fichier>`|Affiche le contenu d'un fichier spécifique dans un commit donné
`git stash`|Mets de côté toutes les modifications
`git stash apply`|Applique les modifications mises de côté
`git status`|Voir les fichiers pas encore commit
`git switch -`|Permet de rattacher la tête à un repo local auquel on l'avait détaché
`git switch -c new_branch_name`|Permet de créer une nouvelle branche à partir d'un repo local avec la tête détachée
`git tag -a v1.2 9fceb02 -m "version 1.2"`|Crée un tag sur un commit
`git tag -d v1.4`|Supprime un tag. Il est supprimé uniquement en local
`git whatchanged`|Affiche l'historique des commits
`set LESSCHARSET=UTF-8 (cmd) ou $env:LESSCHARSET="UTF-8" (powershell) ou LESSCHARSET=UTF-8 (bash)`|Défini l'encodage utilisé par less afin que les accents ne sautent plus. Définir la variable au niveau système pour être tranquille

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

### Faire fonctionner le SSH vers ADO dans WSL

```
# config (~/.ssh/config)
Host azuredevops.septeo.fr
        IdentityFile ~/.ssh/id_rsa
        # IdentitiesOnly yes
        KexAlgorithms diffie-hellman-group1-sha1,diffie-hellman-group14-sha1
        Ciphers +aes128-cbc
        
# test :  should write not implemented/available error (simply test key exchange)
ssh -T git@{FQDN}

# verbosity test
ssh -vT git@{FQDN}

# fix ssh key exchange issue (ubuntu/debian based): 
sudo ip li set mtu 1400 dev eth0
```

> Ne pas oublier de changer l'URL du remote ex `git remote set-url origin ssh://...`


### Utiliser plusieurs comptes GIT sur un même poste

Utile quand on bosse depuis son PC perso et qu'on veut pas flinguer sa configuration perso.

Editer le fichier *~/.gitconfig*, ajouter une section `user` si elle n'existe pas déjà et ajouter une section `includeIf`

```ini
[user]
	email = email.personnel@mail.com
	name = pseudo
[includeIf "gitdir:~/source/repos/boulot/"]
	path = ~/source/repos/boulot/.gitconfig
```

Créer un fichier *~/source/repos/boulot/.gitconfig* et ajouter une section `user` dedans

```ini
[user]
	email = email.professionnel@entreprise.fr
	name = Prénom Nom
```

Les valeurs contenues dans le fichier *~/source/repos/boulot/.gitconfig* écrasent la configuration globale quand on se trouve dans un repo sous *~/source/repos/boulot/*
	
### Compter le nombre de lignes de code

Installer le package CLOC (Count Lines Of Code).
	
```bash
$ sudo apt update
$ sudo apt install cloc
```
	
Ensuite exécuter CLOC sur le répertoire à scanner
	
```bash
$ cloc .
      10 text files.
      10 unique files.
       4 files ignored.

github.com/AlDanial/cloc v 1.82  T=0.19 s (37.3 files/s, 836.4 lines/s)
-------------------------------------------------------------------------------
Language                     files          blank        comment           code
-------------------------------------------------------------------------------
Bourne Shell                     3             17             12             54
Markdown                         1             21              0             39
YAML                             1              0              0              6
DOS Batch                        2              2              0              6
-------------------------------------------------------------------------------
SUM:                             7             40             12            105
-------------------------------------------------------------------------------
```

### Utiliser VSCode comme outil de merge

Ajouter dans `.gitconfig` :
	
```config
[merge]
  tool = code
[mergetool "code"]
  cmd = code --wait --merge $REMOTE $LOCAL $BASE $MERGED
```

Exécuter la commande `git mergetool` à chaque fois qu'il y a des conflits à résoudre.
	
> Remarque : VSCode n'est vraiment pas terrible comme outil de merge
	
### Utiliser p4merge comme outil de merge et de diff

Ajouter dans `.gitconfig` :
	
```config
[diff]
  	tool = p4merge
[merge]
  	tool = p4merge
[mergetool]
	keepBackup = false
```
	
> keepBackup = false permet de supprimer automatiquement le fichier .orig généré par mergetool
	
Exécuter la commande `git mergetool` à chaque fois qu'il y a des conflits à résoudre.
	
Exécuter la commande `git difftool` pour afficher les diffs en cours dans p4merge (ça évite de devoir obligatoirement ouvrir VSCode ou VStudio).

> Si une invite bash GIT est ouverte au moment de l'installation de p4merge, il faut la fermer et en ouvrir un autre afin de bénéficier de la mise à jour des variables d'environnement.

### Supprimer les branches locales qui ne sont plus suivies

`git fetch -p ; git branch -r | awk '{print $1}' | egrep -v -f /dev/fd/0 <(git branch -vv | grep origin) | awk '{print $1}' | xargs git branch -D`

Source : https://stackoverflow.com/questions/13064613/how-to-prune-local-tracking-branches-that-do-not-exist-on-remote-anymore

### Lister les commits créés depuis le dernier tag

Bien utile lors de la préparation du fichier `releases.md`.

`git fetch && git log --oneline --decorate-refs-exclude=refs/heads --decorate-refs-exclude=refs/remotes --decorate-refs-exclude=HEAD $(git describe --tags --abbrev=0)..origin/main`
