# NuGet cheat sheet

## Créer un package et lui attribuer un numéro de version

```bash
dotnet pack -p:PackageVersion=2.1.0 -c:Release
```

## Lister les sources nuget

```bash
nuget sources
```

## Supprimer une source

```bash
nuget sources remove -name <nuget_source_name>
```

Peut s'avérer utile quand une source n'est plus valide et provoque des erreurs d'authentification (401 Unauthorized).
