Vérifier l'existence d'une clef SSH :

```bash
ls -al ~/.ssh
```

Si une clef SSH existe déjà l'utiliser, sinon poursuivre.

Générer une nouvelle paire de clefs SSH :

```bash
ssh-keygen -t ed25519 -C "<email.github@provider.com>"
```

Démarrer l'agent SSH :

```bash
eval "$(ssh-agent -s)"
```

Inscrire la clef SSH sur le poste :

```bash
ssh-add ~/.ssh/id_ed25519
```

Afficher la clef publique :

```bash
cat ~/.ssh/id_ed25519.pub
```

Copier/Coller la clef publique sur github.com.

Cette commande permet de tester le bon fonctionnement de la clef SSH :

```bash
ssh -T git@github.com
```

Cloner le repo en utilisant l'URL SSH :

```bash
git clone git@github.com:<username>/<repo>.git
```

> Dans un repo déjà cloné il faut supprimer le remote et le recréer en utilisant l'URL SSH
> ```bash
> git remote remove origin
> git remote add origin git@github.com:<username>/<repo>.git
> ```
