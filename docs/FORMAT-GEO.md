# Format des cartes .geo VocaRace

Le fichier .geo est un document JSON UTF-8. Le lecteur actuel prend en charge le format **vocarace.geo.v1** avec **version: 1**. Les coordonnées (x, y, width, height) sont exprimées en pourcentage de l’image d’origine : elles ne doivent pas être stockées en pixels écran.

## Structure

- **format** : valeur obligatoire vocarace.geo.v1.
- **version** : version numérique du schéma, actuellement 1.
- **id, name, title** : identifiant interne et noms de la carte.
- **description, instructions** : texte affiché dans la sélection et pendant l’exercice.
- **image** : contient filename, mimeType, width, height et dataUrl. Pour un fichier public transportable, dataUrl doit intégrer l’image. Les images matricielles sont compressées à l’import dans l’atelier ; les SVG sont conservés en data URL.
- **items** : éléments interactifs placés sur l’image. Chaque id doit être unique.

### Éléments pris en charge

Une figure est un point à localiser :

~~~json
{
  "id": "paris",
  "type": "figure",
  "label": "Paris",
  "x": 51,
  "y": 35,
  "tolerance": 7,
  "answers": ["Paris"]
}
~~~

x et y correspondent au centre du point. tolerance est un rayon de tolérance en pourcentage de la carte utilisé par l’exercice de placement ; il est facultatif. answers est une liste facultative de variantes textuelles pour un futur exercice de réponse libre.

Une zone de texte est un rectangle à retrouver :

~~~json
{
  "id": "atlantique",
  "type": "text",
  "label": "Océan Atlantique",
  "text": "Océan Atlantique",
  "x": 2,
  "y": 52,
  "width": 21,
  "height": 13
}
~~~

x et y sont le coin supérieur gauche du rectangle. width et height sont ses dimensions en pourcentage. Les tailles minimales gérées par l’éditeur sont de 5 %.

## Exemple minimal valide

Le fond peut être un SVG intégré, ce qui permet de créer un exemple autonome sans fichier image séparé :

~~~json
{
  "format": "vocarace.geo.v1",
  "version": 1,
  "id": "exemple",
  "name": "Exemple",
  "title": "Une carte de démonstration",
  "description": "Carte très simple.",
  "instructions": "Trouve le point A puis la zone B.",
  "image": {
    "filename": "fond.svg",
    "mimeType": "image/svg+xml",
    "width": 100,
    "height": 100,
    "dataUrl": "data:image/svg+xml;charset=utf-8,%3Csvg%20xmlns%3D%22http%3A%2F%2Fwww.w3.org%2F2000%2Fsvg%22%20width%3D%22100%22%20height%3D%22100%22%20viewBox%3D%220%200%20100%20100%22%3E%3Crect%20width%3D%22100%22%20height%3D%22100%22%20fill%3D%22%23edf4f8%22%2F%3E%3C%2Fsvg%3E"
  },
  "items": [
    {"id": "point-a", "type": "figure", "label": "Point A", "x": 35, "y": 40},
    {"id": "zone-b", "type": "text", "label": "Zone B", "text": "Zone B", "x": 60, "y": 60, "width": 25, "height": 15}
  ]
}
~~~

## Publier une carte dans le jeu

1. Crée ou exporte le fichier .geo depuis l’atelier créateur.
2. Ajoute-le au dossier geo/ du dépôt.
3. Ajoute son chemin exact dans le tableau geo/geo_lists.json.
4. Vérifie que le JSON est valide et que les coordonnées sont comprises entre 0 et 100.
5. Ouvre le mode Géographie et teste les trois exercices compatibles.

Le lecteur expose les trois exercices uniquement si la carte contient les données nécessaires :
- **Identifier une figure** : au moins une figure.
- **Compléter la carte** : au moins une figure.
- **Retrouver une zone de texte** : au moins une zone text.

Les cartes enregistrées dans la bibliothèque privée Firebase ne sont visibles que pour les comptes autorisés. Pour rendre une carte disponible à tous, il faut la publier dans le dépôt et l’ajouter au manifeste public. Ajouter une carte au manifeste n’est pas une opération automatique depuis l’atelier.

## Sécurité et limites

L’éditeur limite la taille des images importées et réduit les images matricielles à une largeur ou une hauteur maximale de 1600 px. Le lecteur valide le format, l’image, les coordonnées et l’unicité des identifiants, mais une validation côté client ne remplace pas une revue du contenu avant publication.
