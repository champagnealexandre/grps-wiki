---
title: "latex"
date: 2017-01-05
weight: 28
description: >
  Présentation des rudiments du langage latex.
---

J’imagine que rendu ici vous êtes tout à fait familiers avec le langage latex.

## Éditeurs

### texpad

[Texpad](https://www.texpad.com) est un éditeur macOS relativement bien conçu qui a deux avantages plutôt pratiques selon moi:

* complétion automatique (ou suggestions) lorsqu’on cite, car il lit les fichiers de bibliographie
* prévisualisation en temps réel du document -- ce qui en fait un outil bien pratique pour rédiger rapidement de petits documents (e.g. lettres, etc.)[^1]

[^1]: À noter que Texpad utilise son outil de compilation interne qui peut ne pas être compatible avec tous les packages latex, et qui peut devenir moins pratique pour les documents plus lourds.

### Overleaf

[Overleaf](https://www.overleaf.com) est un service en ligne qui permet de créer des documents latex et de les visualiser directement dans le fureteur. Se connecte optionnellement avec d’autres services (e.g. Github) ce qui peut être pratique. Possède également des fonctionnalités de collaboration entre auteurs.

### emacs

[Emacs](../../outils/terminal#emacs) est l’un des grand-pères du "Notepad" traditionnel en fonctionne dans le terminal. Il peut évidemment servir à éditer des documents latex, et possède par ailleurs certaines extensions destinées précisément à ça ([auctex](https://www.gnu.org/software/auctex/), par exemple).

Deux avantages importants de `emacs`:

* il s’exécute via le terminal, donc possible de travailler à distance (e.g. via `ssh`) facilement
* il possède d’innombrables raccourcis clavier (qui sont personnalisables), ce qui permet d’accélérer beaucoup l’édition de fichiers

