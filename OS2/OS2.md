º---
title: "OS2"
author: [Vincent Trinh]
date: 15 Février 2018
...

# Operating system 1

* Numéro: 1
* Prof: Gabriel Laskaar
* Date: 15 février 2018

## Correction Contrôle
### what is the purpose of paging in a os?
Isoler les process entre eux, donner des autorisations

### How the pagefault handler of a modern operating system works?
Flemme d'écrire ce qu'il dit.

```
.section ksyms
Cette directive signifie rentrer dans la section ksyms
.size
La taille d'un symbole
```


***
# 22 février 2018
---
## Virtualisation, a quoi ça sert etc

* Machine virtuelle etc
Refaire marcher un système matériel

On virtualise à plein d'endroit : virtualisation de mémoire par exemple.
But: Exposer à l'utilisateur qqc qui ressemble a de la mémoire mais c'est pas la même chose pour isoler. Avoir au final des performances qui ont la même vitesse que s'il n'y a pas les couches.

Principe: Traduire les adresses d'une maniere ou d'une autre et elles se comportent comme les autres. C'est la même chose que la mémoire.

Ce qu'on veut faire:
* être capable de lancer un kernel en userland

Quand on execute un kernel en userland normalement, ca marche bien mais ca casse au bout d'un moment (très vite d'ailleurs). Il y a deux types de reistres: les types généraux et les types sensibles (de configuration) ils contiennent la config du processeur.
Instructions sensibles et générales. Sensible : lit et écrit dans un registre de configuration.
Instructions privilégiés: utilisables qu'en mode superviseur.
Ca va commencer a casser quand on utilise les instructions privilégiés.

Les devices: Un OS attend a avoir des devices.
Principe: Ca s'utilise plus ou moins de la même manière. Il y a des zones de RAM et des zones sur les devices.

Si on peut faire ça, alors l'architecture est virtualisable (a ce point du cours en tout cas)

POurquoi on virtualise? Pour le fric. On achète une machine et on met un service dessus. Quand on veut un autre service, on en achète une autre etc.

Ce serait bien de virtualiser sur des machines user friendly (aka x86)
Ce qu'ils font? On a des instructions sensibles non privilégiés. On lit les instructions a l'avance, et on les patch et on lance le tra.

Autre solution: Modifier l'OS. et ne pas appeler les instructions problematiques, et on les remplace par des hypercalls.
-> C'est de la triche. (qui est un fléau d'ailleurs.)

Conteneurs 
