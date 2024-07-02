# Regex cheat sheet

`()` : groupe

```regex
debut(.*)fin
```
vs
```regex
debut(.*?)fin
```

`.*` = match le plus large (eager)

> **debut blabla fin blublu debut ble ble fin**

`.*?` = match le plus petit (lazy)

> **debut blabla fin** blublu **debut ble ble fin**

```regex
(\d{2})(\.\d{2}){4}.(\1)
```

> 01.02.**12.13.14.15.16.12**.03

`(\1)` => le contenu du groupe doit être identique au contenu du groupe 1

`"(?![0-9]).+?"` => Rechercher toutes les chaines de caractères (entre guillements) ne commençant pas par un chiffre
