# VocaRace
## [Vocarace](https://chevrichon.github.io/VocaRace/) is a way to learn  while playing
The game is made by an ai right now but I'm coding right now an hand made version as my first coding project that actually look like something (base game is implemented).
## Add words lists
To add a word list to the game just do it in the [Pull requests](https://github.com/chevrichon/VocaRace/pulls), for the format just look a the test.espagnol and lists.json files

## Add history date lists
To add a history list, put a `.histoire` file at the repository root. Use one entry per line in the format `date::event`, for example:

```text
14/07/1789::Prise de la Bastille
2 juin 2777::Exemple de date écrite en toutes lettres
```

Then add the exact filename to `histoire_lists.json`:

```json
[
  "histoire.histoire",
  "another-list.histoire"
]
```

The Dates mode reads the list of available files from `histoire_lists.json`. Players can also import their own `.histoire` file directly from their device.

## Géographie et cartes .geo

Le mode Géographie propose trois exercices, selon les éléments contenus dans la carte : identifier une figure, compléter la carte en plaçant une étiquette et retrouver une zone de texte.

Les cartes publiques sont déclarées dans [geo/geo_lists.json](geo/geo_lists.json). Un exemple jouable se trouve dans [geo/France-villes.geo](geo/France-villes.geo). Les cartes doivent respecter le schéma versionné **vocarace.geo.v1** documenté dans [docs/FORMAT-GEO.md](docs/FORMAT-GEO.md).

Pour publier une carte :

1. Crée-la dans l’atelier créateur, puis télécharge le fichier .geo.
2. Place le fichier dans le dossier geo/.
3. Ajoute son chemin au tableau geo/geo_lists.json.
4. Vérifie le rendu dans le mode Géographie avant de publier le changement.

La bibliothèque de l’atelier reste privée. Les fichiers privés ne sont pas publiés automatiquement pour les joueurs ; il faut les ajouter explicitement au dépôt public pour les rendre accessibles à tous.

### Règles Firebase de l’atelier

Les changements de permissions doivent également être publiés dans Firebase Console → Realtime Database → Rules à partir du fichier database.rules.json. Modifier le fichier dans GitHub ne déploie pas automatiquement ces règles dans le projet Firebase.
