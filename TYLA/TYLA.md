---
author: trinh_v
title: Typologie des Langages
...

# Typologie des Langages

* Etienne Renault

## Culture Générale

* Début des machines à calculer: L'Homme a toujours commencé par détruire ce qu'il
découvre. Du coup, on comptait les morts en comptant les cailloux.
* Abac: Ancêtre du boulier
* Pascaline
* Babbage Calculer les tables de Nautique.

# 2018-04-25 //FIXME ABSENT

* fortran calculs scientifiques
* algol
* kobol langage business sûr pour l'armée

# 2018-04-26

Maintenant, on veut fusionner les 3 langages.Le problème est de faire quelque chose
performant, en gérant l'orthogonalité des langages (virtual et templates...)

## PL/I

## ADA

Il a introduit les variables readonly / write only, les interruptions, les exceptions
et une clock. Il y a donc un quantum de temps exécuté.

## K.N. King

C'est un forceur.

# Historique Orienté Objet.

Idée de base du langage objet est de tout regrouper.

## SIMULA

* Ole-Johan Dahl & Kristen Nygaard
* Ils ont voulu introduire une notion de temps (threads) pour chaque "objet" (qui
  n'existent pas encore)
* Construit en désucrant, langage intermediaire: algol 60
* introduction du concept d'objet et de classe.

## Smalltalk

Pousser le concept d'objet

> We called Smalltalk smalltalak so that nobody would expect anything from it
> > Alan Kay

* Tout est object
* Passage par messages
* LE comportement de l'objet est décrit par sa classe.
* if, while seront des objets.

Règles:

* Tout est objets
* Toutt est une instance de classe
* Toute classe possède 1 superclasse
* Tout fonctionne via des passages par messages.
* Le lookup se fait suivant la chaîne d'héritage
* Chaque classe est une instance d'une métaclasse
* La hiérarchie d'une métaclasse est parallèle à la hiérarchie des classes
* Chaque classe hérite de Class
* Chaque métaclasses est une instance de Metaclass
* La métaclasse de Metaclass est une instance de Metaclass

```
x := 100@200
Classe de x : point
Classe de point: Point Class
classe de Point Class: Metaclass
Classe de Metaclass: Metaclass Class
Classe de Metaclass class: Metaclass
Superclasse de x: Object
Superclass de point class: Object Class
```

## Objective-C, pascal, C++

* Envoie des messages aux objets pour appeler des méthodes.
  - pas très performant
  - Facile à faire de la distribution.
* CLOS: Plus de sélection de methodes
* Eiffel
* C++

## C++ Stroustrup

* namespace


# Subprograms : Fonctions / routines

* Procédures qui ne retournent rien
* Fonctions qui retournent une valeur
