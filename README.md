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
