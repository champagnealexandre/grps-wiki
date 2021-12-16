---
title: "Makefile"
date: 2017-01-05
weight: 22
description: >
  Présentation des rudiments du langage de scripts Makefile.
---

{{% pageinfo %}}
On présente dans cette page quelques exemples de fichiers Makefile pouvant être utiles pour la compilation de documents latex, codes C, etc.
{{% /pageinfo %}}

Un script Makefile est à bien des égards similaire à un [script Bash](../bash), mais possède une syntaxe parfois légèrement différente. Les scripts Makefile sont exécutés non pas par `bash` mais par `make`, et servent de manière générale à compiler des objets.

## Exemple: compilation d’un document LaTeX

> On peut se servir d’un Makefile pour compiler automatiquement et rapidement un document latex.

Par exemple, on peut se servir d’un script de ce genre pour compiler un document latex:

```makefile
.IGNORE:

default:
    pdflatex <document-name>
    chflags -R hidden *.aux *.bbl *.blg *.log *.out *.lof *.lot *.toc 
bib:
    pdflatex <document-name>
    bibtex <document-name>
    pdflatex <document-name>
    pdflatex <document-name>
    chflags -R hidden *.aux *.bbl *.blg *.log *.out *.lof *.lot *.toc 

clean:
    rm -r *.aux *.bbl *.blg *.log *.out *.lof *.lot *.toc
```

En copiant le texte ci-dessus dans un fichier sans extension nommé `Makefile` (notez le `M` majuscule), on peut alors taper les commandes suivantes dans le répertoire où se trouve le fichier pour exécuter les commandes associées du Makefile:

* `make` : exécute la section `default` (compile le fichier latex)
* `make bib` : exécute la section `bib` (compile le fichier latex et la bibliographie)
* `make clean` : exécute la section `clean` (nettoie le répertoire des fichiers temporaires)

## Exemple: compilation d’un code C

> Un exemple un peu plus élaboré: conception d’un Makefile pour compiler un code C à l’aide de `gcc`.

On peut aussi se servir d’un Makefile pour compiler un code C. Par exemple, le script suivant compile mon code de calcul selon le système d’exploitation (la procédure de compilation diffère de l’un à l’autre):

```makefile
CXX		:= g++
RM		:= rm -f
CPPFLAGS	:=
LDFLAGS		:= -O2 -fmax-errors=5 -fcompare-debug-second
LDLIBS-MACOS	:= -I/usr/local/include -L/usr/local/lib -lgsl
LDLIBS-CENTOS	:= -I/home/alexandre/lib/gsl/include -L/home/alexandre/lib/gsl/lib -lgsl -lgslcblas

SRC_DIR		:= src
SRCS		:= $(wildcard $(SRC_DIR)/*.cpp)
BUILD		:=build/clipd
LATEST_VERSION	:=3

all:
	@echo MacOS or CentOS?
	@exit 1
version_check:
ifdef v
else
	$(eval v=$(LATEST_VERSION))
	@echo No version specified, making version $(v)
endif
macos: version_check
	@echo Building for MacOS...; echo ""
	$(CXX) $(LDFLAGS) $(LDLIBS-MACOS) $(SRC_DIR)$(v)/*.cpp -o $(BUILD)$(v)

centos: version_check
	@echo Building for CentOS...; echo ""
	$(CXX) $(LDFLAGS) $(LDLIBS-CENTOS) $(SRC_DIR)$(v)/*.cpp -o $(BUILD)$(v)

clean:
	$(RM) $(BUILD)*
```

On peut alors se servir soit de `make macos` ou de `make centos` afin de compiler le code.

