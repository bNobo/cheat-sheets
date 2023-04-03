# Powershell Cheat Sheet

Commande | Description
--- | ---
`$env:HTTP_ECHO_PORT=8080`|Set une variable d'environnement
`rmdir folder -force`|Supprime un répertoire même s'il n'est pas vide
`Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux`|Active WSL ce qui permet d'éviter une erreur "WslRegisterDistribution failed with error: 0x80004002" au démarrage de Linux. Attention il faut également activer la fonctionnalité Windows "Plateforme de machine virtuelle".
