# IIS cheat sheet

## Modification de variable d'environnement

Si vous modifiez une variable d'environnement, la modification n'est pas prise en compte tant que le serveur n'est pas redémarré. 

Recycler le pool d'applications, redémarrer le site ou même rémarrer le serveur IIS ne suffit pas. Il faut redémarrer physiquement la machine.

Ou, pour éviter cela, ouvrir une invite en mode administrateur et taper la commande `iisreset /restart`.
