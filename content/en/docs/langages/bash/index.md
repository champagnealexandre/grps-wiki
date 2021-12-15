---
title: "Bash"
date: 2017-01-05
weight: 21
description: >
  Présentation des rudiments du langage de scripts bash.
---

L’utilisation de scripts `bash` (ou son alternative, `zsh`) est un moyen pratique d’automatiser une foule de tâches dans un environnement *nix (linux, macOS, etc.) -- du lancement automatique de codes de calcul à l’exécution de tâches de maintenance.

## Creation d’un script

Un script `bash` est simplement un fichier texte exécutable qui comporte optionnellement une extension `.sh`. Pour créer le script `test.sh` et le rendre exécutable, on peut faire:

```shell
touch test.sh
chmod 700 test.sh
```

On doit ensuite inscrire la ligne suivante au début du fichier:

```bash
#/usr/bin/env bash
```

Chaque ligne d’un script bash est ensuite simplement exécutée comme si elle était entrée manuellement à l’invite de commande.

On peut également se servir de tests conditionnels pour diriger l’exécution de script,

```bash
if [[ -z "$string" ]]; then
  echo "String is empty"
elif [[ -n "$string" ]]; then
  echo "String is not empty"
fi
```

de variables,

```bash
NAME="John"
echo $NAME
echo "$NAME"
echo "${NAME}!"
```

etc.