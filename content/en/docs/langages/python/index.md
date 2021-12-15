---
title: "Python"
date: 2017-01-05
weight: 23
description: >
  Présentation des rudiments du langage Python.
---

Vous êtes probablement déjà relativement familier avec Python, donc je ne m’étendrai pas sur le détail de la syntaxe. Toutefois, quelques informations pertinentes peuvent être mentionnées ici.

## Environnements

### Anaconda

[Anaconda](https://anaconda.org) est probablement la distribution la plus populaire du langage Python, disponible sur plusieurs plateformes.

On peut y créer des environnements virtuels qui comportent une configuration précise (packages présents, etc.) en faisant:

```shell
conda create -n my-env
conda activate my-env
```

Pour installer un module:
```shell
conda install <module>
```

Pour ajouter un répertoire au `PYTHONPATH`, ce qui permet de créer soi-même des modules:
```shell
conda develop <dir>
```

## Packages utiles

* **numpy** : se passe de présentation.
* **matplotlib** : idem.
* **scipy** : idem.
* **click** : permet de créer facilement des interfaces de ligne de commande.
* **pickle** : lecture/écriture disque d’objets en mode binaire.
* **tqdm** : création de barres d’avancement en ligne de commande.
* **numba** : permet de précompiler du code Python, ce qui accélère énormément sa vitesse d’exécution[^1].

[^1]: Dans la réalité, `numba` peut être très efficace pour accélérer des algorithmes très simples qui nécessitent peu de lignes de code et le moins de packages possible, mais son utilisation devient très difficile pour des codes plus longs, qui font appel à des packages externes ou du code orienté objet. De plus, les messages d’erreur de `numba` sont des plus cryptiques, donc bonne chance pour débugger votre code.

## Interface avec d’autres langages

On peut interfacer du code Python avec des routines écrites en C ou en Fortran, avec [Cython](https://cython.org) et [F2PY](https://numpy.org/doc/stable/f2py/) respectivement.