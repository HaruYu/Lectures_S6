---
title: "Architecture orienté objet"
author: trinh_v
date: 2018-03-07
...

# Architecture Orienté Objet

* Numero: 1
* Prof: Arnaud Lemettre
* Date: 8 mars 2018

## Interface

*Contrat* qui détermine une classe.

## Raisons d'architecturer en objet?

* Maintenir le code
* Lisibilité
* Rendre le code testable
* Faciliter le développement
* Travailler en groupe
* Être plus efficace

## Architecture N-Tier

Architecture en couche: Interface <-> Business Management <-> DataAccessLayer

Toutes ces parties ont un DBO (data business object). Des getter/setters

Avantages: Si on change le Data access layer, On n'a qu'à changer cette couche et les getters/setters restent les mêmes.

Quand on change le code, essayer le moins de couches possibles.

## Principe de Développement

* KISS
  - Keep it simple, stupid
* YAGNI
  - You aren't gona need it : Ne pas coder des choses useless (Plus de temps a debugger, coder...)
* DRY
  - Don't repeat yourself : Eviter le c/c, evite d'enchainer les if/else et usiliser le polymorphisme a la place.
* SOLID
  - Single Responsibility, Open-close, Liskov substitution, Interface Segregation, Dependency Injection
  - Une classe ne doit avoir qu'une seule responsabilité
  - Une classe doiti pouvoir être étendue mais pas modifiée (ajout de fonctionnalité doit se faire en ajoutant du code et non pas en éditant)
  - Utilisation d'interface pour éviter de mettre des if dans le code (bien que rectangle et carré aient largeur/longueur), il faut ajouter une contrainte sur la largeur/longueur du carré
  - On modifie pas une interface mais on ajoute une nouvelle interface qui hérite de la première
  - Permet de farder une flexibilité du code.

## Design patterns

### Repository

But: Essayer d'éviter de répéter les opérations de base des accès aux données [**C**reate **R**ead **U**pdate **D**elete] **.**

### Fluent API

### Memento

### Decorator

Ajouter des fonctionnalités sans hériter.

## Références

* Design Patterns Elements of Reusable Object-Oriented Software
* [Uses of design patterns](httm://martinfowler.com/)
