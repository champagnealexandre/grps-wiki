---
title: "Grappe de calcul"
date: 2017-01-05
weight: 41
description: >
  Description de la grappe de calcul du groupe de recherche.
---

{{% pageinfo %}}
On présente ici des informations sur la connexion à la grappe de calcul du Groupe, les sépcifications matérielles et logicielles des serveurs, ainsi que quelques scripts utiles.
{{% /pageinfo %}}

## Connexion

> Connexion aux serveurs de grappe de calcul. La procédure détaillée n’est pas présentée puisque ce site est public.

On peut se connecter en [ssh](../../outils/terminal#ssh) aux serveurs de la grappe de calcul.

De l’extérieur du campus, on doit passer par la machine de proxy ou par le VPN de l’Université de Montréal.

## Spécifications matérielles

> Spécifications matérielles des serveurs de calcul de la grappe.

La grappe de calcul consiste en une vingtaine de machines possédant chacune entre 8 et 24 coeurs de processeur, et entre 8 et 32GB de mémoire vive. Votre répertoire de travail est situé sur un disque partagé, donc peu importe la machine où vous vous connectez vous avez accès aux mêmes fichiers, en temps réel.

## Environnement logiciel

> Description de l’environnement logiciel des serveurs de la grappe.

Les serveurs opèrent sous CentOS Linux et possèdent des versions relativement à jour des interpréteurs (Python, etc.) et compilateurs (Fortran, C, etc.)

Les machines n’ont pas d’accès direct à internet.

Vous pouvez y installer des applications dans la mesure où celles-ci ne nécessitent pas d’accès administrateur pour être installées.

## Scripts utiles

> Quelques scripts utiles lors de l’utilisation de la grappe.

### Liste de serveurs

On peut créer une liste de serveurs de la grappe pour e.g. utilisation avec [parallel](../../outils/terminal#parallel) avec un script du style:

```shell
#!/bin/bash

for i in $(seq -f "%02g" 0 23)
do
  ssh -o ConnectTimeout=5 -q sol$i-ib exit > /dev/null
  if [ $? -eq 0 ]
  then
      echo sol$i-ib
  fi

done

echo taranis
```

### Usage des machines

On peut vérifier quel est le pourcentage d’utilisation des processeurs de chacune des machines en exécutant un script tel que:

```shell
#!/usr/bin/env bash

while read -u10 HOST
# do ssh $HOST 'printf "$(hostname): " ; top -n 1 -b | grep %Cpu' &
   do ssh $HOST 'top -n1 -b | grep %Cpu | xargs -d "\n" printf "$(hostname) %s\n"' &
done 10< ~/cluster_hosts.txt

wait
```

