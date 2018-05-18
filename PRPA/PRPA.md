---
author: trinh_v
title: Programmation Parallèle
...

# Introduction au parallelisme
----
[lien](lrde.epita.fr/~carlinet/cours/parallel)
## Pourquoi faire des choses en parallèle?

* Pour le faire plus rapidement.

Il y a trois domaines qui ont besoin de PRPA:

* Mobile. Plus vite on execute, moins on utilise de batterie.
* Big data. Traiter le plus vite possible les datas.
* Systèmes en temps réel: Le temps de réponse doit être rapide.
* Micro-trading.

## Comment rendre les choses plus rapides?

Faire le moins de traitements possible: Choses redondantes, moins de choses,
des choses en même temps, distribuer le travail entre les "travailleurs".

* Trouver les algorithmes les plus efficaces.
* Choisir les structures de données les plus adaptées
* Paralléliser

La programmation parallèle est un outil qui peut rendre un programme plus rapide.
Il doit être une solution, et pas une façon de faire.

| | single instruction | Multiple instruction |
|:---|:------------- | :------------- |
| single data | SISD       | MISD |
|Multiple data   | SIMD  | MIMD  |


Exemple: Chaine d'assemblage de sandwiches (salade, tomate, fromage)

* Les trois workers doivent se synchroniser avant de fermer le pain. C'est pas
 forcément la façon la plus optimisée, il y a besoin de synchronisation.
* Prendre des workers différents qui font 4 pipelines en parallèle.$\rightarrow$ 400% speedup attendus
* Taffer en fonction des taches: threadpools mais implique de la synchronisation
* Un worker qui fait 4 sandwiches en même temps $\rightarrow$ 400% speedup

Sur la majorité des cas, il y aura le dernier cas.

Quand on utilise tous les coeurs vs quand on en utilise qu'un seul: il diminue sa
 fréquence quand on en utilise plusieurs pour éviter de chauffer.

## Exemple

``` cpp
//calculates the sum of the strings (they are ints, so use atoi)
long sum_of_strings(const char* strings[]; std::size_t n);
```

Ce qui merdait, c'était le shuffle.

How to optimize it?

* First bench and profile:
  - google benchmark
  - perf
  - intel studio

L'operation get est long. Dépendant quel cache on va chercher

Faire des programmes cache friendly c'est pas mal.

# Architecture superscalaires

## Instruction Level Parallelism.

## Casser des dépendances pour augmenter le speedup

## ILP: Conclusion

* Casser les dépendances (moins de parenthèses dans les calculs)
* Arranger des branchements différents avec les plus fréquents au dessus

# 2018-04-27

On veut faire du parallelisme car on ne peut plus augmenter la fréquence des processeurs.

## Threads in C++11

std::thread
Join the thread or detach it before destroying it.
