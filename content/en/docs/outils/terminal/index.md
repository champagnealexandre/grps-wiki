---
title: "Terminal"
date: 2017-01-05
weight: 31
description: >
  Aperçu de quelques commandes utiles au terminal.
---

{{% pageinfo %}}
On donne ici une description de quelques outils utiles au terminal. Beaucoup de ces outils sont propres à un environnement *nix (macOS, linux, etc.)
{{% /pageinfo %}}

## ssh

[SSH](https://en.wikipedia.org/wiki/Secure_Shell) est un protocole qui permet de se connecter de manière sécurisée à distance au terminal d’une autre machine, par exemple celles de la grappe de calcul. La plupart des systèmes d’exploitation disposent d’emblée d’une application (normalement appelée `ssh` elle aussi) qui permet la connexion.

Pour se connecter:

```shell
ssh <adresse>
```

On peut aussi enregistrer ses informations de connexion dans la machine distante afin de ne pas avoir à entrer son nom d’utilisateur/mot de passe à chaque fois. Sur sa propre machine, si l’exécution de

```shell
ls -al ~/.ssh/id_*.pub
```

retourne `No such file or directory` ou similaire, on se génère une clé RSA avec

```shell
ssh-keygen -t rsa -b 4096 -C "your_email@domain.com"
```

puis on copie ses informations de connexion sur la machine distante via

```shell
ssh-copy-id remote_username@server_ip_address
```

## git

[Git](https://git-scm.com) est un système de contrôle de version qui permet de gérer les différentes versions (passées, ou alternatives) d’un code, et qui peut agir en même temps comme copie de sauvegarde[^1]. On l’utilise fréquemment avec des services comme [Github](https://github.com) ou [Bitbucket](https://bitbucket.org), qui agissent comme serveur distant sur lesquels les *dépôts* locaux sont sauvegardés. La plupart des systèmes d’exploitation possèdent d’entrée de jeu une version de `git`.

Un "dépôt" git est simplement un répertoire qui contient un sous-répertoire nommé `.git` contenant la configuration du dépôt et les méta-données (historique, etc.) On peut créer un dépôt dans un dossier en faisant:

```shell
git init
```

puis en ajoutant des fichiers au dépôt via
```shell
git add <fichiers>
git commit -m '<message de mise à jour>'
git branch -M main
git remote add origin <repo-url>
git push -u origin main
```

où `<repo-url>` correspond à l’adresse d’un dépôt distant (Github, etc.) que l’on aura précédemment créé.

Chaque fois qu’une modification substantielle doit être sauvegardée (e.g.: vous avez terminé de programmer une fonction importante d’un code), il suffit de `git add` les fichiers, entrer un message de mise à jour via `git commit` puis de pousser les changements sur le serveur via `git push`.

À l’inverse, pour créer une copie locale d’un dépôt distant, on fait

```shell
git clone <adresse du dépôt>
```

Pour voir l’historique de mise à jour d’un dépôt, on peut faire

```shell
git log
```

On peut se servir de git pour suivre les mises à jour d’un code (peu importe le langage de programmation), et même pour sauvegarder/suivre les changements d’un document latex. Un dépôt peut comporter n’importe quel type de fichier, dans la mesure où celui-ci respecte les limites de stockage du serveur.

[^1]: Généralement pour des fichiers texte (e.g. code source). Git ne prend pas en charge les fichiers volumineux, donc ce n’est pas *à proprement parler* une application de sauvegarde.


## parallel

[GNU Parallel](https://www.gnu.org/software/parallel/) est une application qui permet de lancer des processus simultanément sur une machine (local ou distante, via SSH), de manière automatisée, et en permettant une grande flexibilité.

Un exemple de situation où `parallel` est très utile: lancer une série de processus de calcul sur la grappe du groupe de recherche.

Par exemple, on peut se servir d’une commande telle

```shell
parallel --env PATH --workdir . --sshloginfile ~/cluster_hosts.txt --sshdelay 0.1 --bar $@
```

pour lancer une série de processus sur la liste de serveurs contenue dans le fichier `cluster_hosts.txt`.

## curl et wget

`curl` et `wget` permettent respectivement d’afficher dans le terminal et de télécharger des pages web (ou fichiers) présents sur un serveur. Ils sont normalement présents sur une machine *nix sans besoin d’être installés.

Par exemple,

```shell
curl www.google.com
```

affiche le contenu de la page dans le terminal, tandis que

```shell
wget www.google.com
```

télécharge le fichier `index.html` du serveur.

## imgcat

[imgcat](https://pypi.org/project/imgcat/) est un package Python qui peut aussi être directement appelé via la ligne de commande. Il sert à afficher des images (`png`, etc. mais aussi `pdf`) via le terminal. Très pratique e.g. lorsqu’on se connecte à distance sur une machine.

Par exemple,

```shell
imgcat test.png
imgcat test.pdf
```

affiche les fichiers `test.png` et `test.pdf`.

## tar, gzip et (un)zip

Présents d’emblée sur les systèmes *nix, `tar` et `(un)zip` permettent de créer des archives (de dossiers, fichiers) ou d’extraire les fichiers y étant contenus. La commande `zip` crée un fichier compressé "zip", tandis que la commande `tar` ne crée qu’une archive (qui n’est pas compressée). On peut aussi compresser une archive `tar` avec la commande `gzip` afin de créer une archive `.tar.gz` compressée.

Pour créer un fichier zip,

```shell
zip -r <file.zip> <folder> -x <exclude>
```

et pour le décompresser,

```shell
unzip <file.zip>
```

Pour créer une archive tar,

```shell
tar cf <file.tar> <files>
```

et pour en extraire les fichiers,

```shell
tar xf <file.tar>
```

Finalement, pour compresser une archive tar avec `gzip`,

```shell
gzip <file>
```

et pour la décompresser,

```shell
gzip -d <file.gz>
```

## brew

[Brew](https://brew.sh) est un gestionnaire d’applications pour macOS (similaire à `yum` et autres sous linux) qui contient une grande quantité d’outils.

Par exemple, pour installer `emacs` on peut faire

```shell
brew install emacs
```

## emacs

[Emacs](https://www.gnu.org/software/emacs/) est l’un des grand-pères du "Notepad" traditionnel en fonctionne dans le terminal. Normalement présent d’emblée sur les postes *nix, il peut aussi être mis à jour (puisqu’il est toujours activement développé).

Deux avantages importants de `emacs`:

* il s’exécute via le terminal, donc possible de travailler à distance (e.g. via `ssh`) facilement
* il possède d’innombrables raccourcis clavier (qui sont personnalisables), ce qui permet d’accélérer beaucoup l’édition de fichiers

## vi

`vi` est le frère d’`emacs`, et permet également d’éditer rapidement des fichiers textes. Choisir entre `emacs` et `vi` est une question de préférence personnelle (mais `emacs` est *définitivement* supérieur).

Présent également d’emblée sur les postes *nix.

## time

Permet de mesurer le temps d’exécution d’une commande.

e.g.

```shell
time ls -R . > /dev/null
```

retourne quelque chose comme

```shell
ls -R . > /dev/null  4.44s user 5.10s system 62% cpu 15.152 total
```

Le temps `total` est le temps "réel" pris par la commande pour être utilisée (ici, 15.152 sec)