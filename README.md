# TGDev.Portfolio — Blazor WebAssembly

Portfolio de Thomas Gourdet, en Blazor WebAssembly (.NET 8, standalone). Animation du terminal du hero est pilotée en C# (`PeriodicTimer` + `StateHasChanged`).

## Prérequis

- [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

## Lancer en local

```bash
dotnet restore
dotnet run
```

Le site est servi sur `https://localhost:5001` (ou l'URL affichée dans la console).

## Compiler pour la production

```bash
dotnet publish -c Release
```

Les fichiers statiques prêts à déployer se trouvent dans :
`bin/Release/net8.0/publish/wwwroot`

C'est ce dossier qu'il faut héberger — pas le dossier `wwwroot` du projet source.

## Déployer sur GitHub Pages

Blazor WebAssembly produit un site 100% statique, donc GitHub Pages fonctionne, avec 3 ajustements propres aux apps Blazor :

1. **`<base href>`** — dans `wwwroot/index.html`, remplace `<base href="/" />` par `<base href="/NOM-DU-DEPOT/" />` si le site est publié sur `https://<pseudo>.github.io/NOM-DU-DEPOT/` (pas nécessaire si le dépôt s'appelle `<pseudo>.github.io`).
2. **`.nojekyll`** — ajoute un fichier vide nommé `.nojekyll` à la racine du contenu publié. Sans lui, GitHub Pages (qui passe par Jekyll) ignore le dossier `_framework`.
3. **Fallback SPA** — copie `index.html` en `404.html` dans le dossier publié, pour que le rafraîchissement d'une URL profonde (ex: après navigation) ne renvoie pas une 404 GitHub.

Séquence type :

```bash
dotnet publish -c Release
cd bin/Release/net8.0/publish/wwwroot
touch .nojekyll
cp index.html 404.html
# pousser ce dossier vers la branche gh-pages (ou le dossier /docs de main)
```

Ensuite, dans Settings > Pages du dépôt, choisis la branche/dossier qui contient ces fichiers.

## Structure

```
TGDev.Portfolio.csproj
Program.cs
App.razor
Layout/MainLayout.razor
Pages/Portfolio.razor   ← contenu du portfolio
wwwroot/index.html
wwwroot/css/portfolio.css
```
