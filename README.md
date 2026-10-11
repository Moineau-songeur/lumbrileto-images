# Images en ligne du forum (`lumbrileto-images`)

Les images que le forum affiche. Elles ne peuvent pas vivre dans le dépôt du code
(`refonte-claude`) : celui-ci est **privé**, et jsDelivr — le service qui sert ces
fichiers au forum — ne distribue que des dépôts **publics**.

D'où deux dépôts, dans un seul dossier sur le Bureau :

| | Dépôt | Visibilité | Contient |
|---|---|---|---|
| le dossier parent | `Lumbrileto` | privé | le code du forum |
| ce dossier-ci | `lumbrileto-images` | **public** | seulement des images |

Ce dossier est ignoré par le dépôt privé (voir son `.gitignore`) : il se commite et
se pousse **chez lui**, séparément.

## Ce qu'il y a dedans

| Fichier | Sert à |
|---|---|
| `etoile-forme.svg` | La silhouette de l'étoile, utilisée partout en découpe (puces de catégories, compteurs de la liste des sujets, profils). Appelée par `--forme-etoile` dans `src/css/01-tokens.css`. |
| `etoile.svg`, `etoile2.svg` | Deux premiers essais d'export, gardés comme trace. **Rien ne s'en sert.** |

## Ajouter une image

1. Déposer le fichier dans ce dossier.
2. Depuis ce dossier, publier :

```powershell
git add .
git commit -m "Ajoute <nom du fichier>"
git push origin main
```

3. Son adresse sur le forum est alors, en remplaçant le nom du fichier :

```
https://cdn.jsdelivr.net/gh/Moineau-songeur/lumbrileto-images@main/etoile-forme.svg
```

**Attendre quelques minutes** après le `git push` : jsDelivr met le temps de
recopier le fichier avant que l'adresse réponde.

## Le piège : remplacer une image existante

Si on remplace une image **en gardant le même nom**, l'adresse ne change pas — et
jsDelivr continue de servir l'ancienne version, jusqu'à **12 heures**. Deux façons
de s'en sortir :

- **Le plus simple : donner un nouveau nom au fichier** (`etoile-forme-2.svg`), et
  mettre à jour l'adresse dans le CSS. Effet immédiat, aucune surprise.
- Ou vider le cache en ouvrant cette adresse dans le navigateur (le chemin du
  fichier, précédé de `purge.jsdelivr.net`) :

```
https://purge.jsdelivr.net/gh/Moineau-songeur/lumbrileto-images@main/etoile-forme.svg
```

## Ce qui ne doit jamais entrer ici

Ce dépôt est **public** : tout ce qu'on y dépose est visible de n'importe qui. Donc
des images, et rien d'autre — jamais de code du forum, de page copiée depuis
l'administration, ni de capture d'écran où apparaît un identifiant.
