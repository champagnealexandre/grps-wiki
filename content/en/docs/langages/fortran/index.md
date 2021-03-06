---
title: "Fortran"
date: 2017-01-05
weight: 25
description: >
  Présentation des rudiments du langage Fortran.
---

{{% pageinfo %}}
On présente dans cette page quelques informations concernant le langage de programmation Fortran, les moyens de l’interfacer avec Python, et un bref exemple introductif.
{{% /pageinfo %}}

{{< alert color="warning" >}}Je connais très peu le Fortran, donc page à rédiger éventuellement.{{< /alert >}}

Le principal attrait du Fortran est qu’il est, comme le C, un langage compilé. Ceci signifie que sa vitesse d’exécution est bien supérieure à votre Python habituel.

La syntaxe générale de Fortran est relativement simple, et il est encore beaucoup utilisé dans plusieurs groupe de recherche vu sa popularité dans les années 80-90.

On peut notamment utiliser [F2PY](https://numpy.org/doc/stable/f2py/) pour interfacer du code Python avec du code Fortran -- donc "inclure" des routines Fortran dans un code d’analyse Python plus large, par exemple.

## Exemple introductif

> Syntaxe et compilation d’un exemple minimal de type "hello world".

Un code Fortran de type "hello world" pourrait ressembler à:

```fortran
program hello
  ! This is a comment line; it is ignored by the compiler
  print *, 'Hello, World!'
end program hello
```

On peut le compiler à l’aide de

```shell
gfortran -o hello hello.f90
```

ce qui produit l’exécutable `hello`.

