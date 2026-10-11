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
| `fond-bann-clair.svg` | Le décor de nuages derrière le bandeau de la page d'accueil, **version claire**. |
| `fond-bann-sombre.svg` | Le même décor, **version sombre**. Les deux ne diffèrent pas que par la teinte des nuages : les traits sont noirs ici, blancs dans la version claire. |
| `fond-bann-saison.svg` | Sa **version saisonnière**. Copie conforme de la sombre pour l'instant, à recolorier quand tu voudras. |
| `cadre-avatar.svg`, `cadre-liste-membre.svg`, `chouette.svg`, `nuage.svg`, `soleil-nuage-titre.svg` | Déposés, publiés, mais **pas encore appelés** par le forum. |

## La règle des noms : `dessin-thème.svg`

Un même dessin peut exister en trois versions, une par ambiance du forum :

```
fond-bann-clair.svg     fond-bann-sombre.svg     fond-bann-saison.svg
```

Les suffixes reconnus sont **`-clair`**, **`-sombre`** et **`-saison`**. Un fichier
sans suffixe (`nuage.svg`) est une version unique, la même pour les trois thèmes.

C'est cette règle qui permet à l'outil du simulateur (*Couleurs des SVG*) de
regrouper les versions d'un dessin, de passer de l'une à l'autre, et d'en créer
une qui manque à partir d'une autre. **Changer une version ne touche jamais les
autres** : ce sont trois fichiers distincts.

Si tu renommes un fichier, pense à l'adresse qui le désigne dans le CSS : elle
contient le nom.

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
