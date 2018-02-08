# Théorie des Graphes

## Introduction


* 1735 Euler
* 7 ponts de Koringsberg -> Est-il possible de faire une promenade pour traverser chaque ponts une seule fois? Non c'est pas possible.

![7pts](7pts.png)
Deg(s2)=5
Deg(s1)=3
Deg(s4)=3
Deg(s3)=3

Un **multigraphe** peut avoir plusieurs fois une arrête reliant deux sommets

A chaque fois qu'on passe par un sommet, on utilise une arete pour entrer et une pour sortir sauf pour les sommets initiaux et finaux.
**=>** Si un chemin eulérien existe, il faut nécessairement qye ke nombre de sommets de degré impaire
* soit 0 (si arrivée = départ)
* soit 2 (si l'arrivée != départ)

**=>** il n'existe pas de solution aux 7 ponts de K.

### Théorèmes
* Un multigraphe non orienté possède un cycle eulérien si et seulement si tous ses sommets sont de degré pair et les sommets de degré > 0 sont dans la même **composante connexe**
* S'il y a deux sommets de degré impair, alors il existe un chemin eulérien

### Algorithme pour produire un cycle eulérien dans un graphe connexe dont tous les sommets sont pairs

![k5](k5.png)
Graphe K5

1. Choisir un sommet (départ) construire un chemin a partir de ce sommet en effacant les arêtes au fur et a mesure. Comme les sommets sont de degré pair, on peut toujours avancer jusqu'à retomber sur le sommet de départ où on s'arrête.
  * a -> b -> d -> e
2. Dans les arêtes qui restent, l'un des sommet est forcément sur le chemin créé car le graphe est connexe
3.  Etape 1 a partir de ce sommet
  * b->c->e->d
4. Insérer le cycle dans le chemin
  * a->**b->c->e->b**->d->e->a
5. Répéter 2-3-4 jusqu'à ce qu'il n'y ai plus d'arrête.
  * a->c->d->a
  * a->c->d->a->b->c->e->b->d->e->a

## 1847 : Kirchhoff

Arbre recouvrant : un arbre qui recouvre le graphe

## 1860 : Cayley

Énumérer des isomères d'alcanes
```
n=1 1 isomère
n=2 1 isomère
n=3 1 isomère
n=4 2 isomères
n=5 3 isomères
n=6 5 isomères
n=7 9 isomères
n=8 18 isomères
    35
    75
    155
    355
```

Un alcane = 1 arbre avec n carbones et x hydrogènes
on veut montrer que x = 2n+2

n+x sommets
n+1-1 arêtes <- Propriété: Un arbre de n sommets possède n-1 arêtes  

### Propriété
La somme des degrés de tous les sommets = 2 * le nombre d'arêtes.

Somme(v dans V, [deg(v)]) = 2 * |E|
Somme(v dans V, [deg(v)]) = 2 * (n + x - 1)
4n+x = 2n + 2x -2
**2n+2 = x**

**propr** Le nombre de sommets de degré impair est pair
**preuve** Somme(v dans V, [deg(v)]) = 2* |E| est pair

### La formule de Cayley

Le nombre d'arbre (*graphe acyclique et connexe*) (sans racine) de sommets numérotés est n^(n-2)

#### Demonstration (cf: Wikipedia)

### Théorème
Le nombre d'arbres couvrants d'un graphe G est égal à la valeur absolue de n'importe quel cofacteur de la matrice laplacienne de G

La matrice laplacienne
`` L = D - M ``
D= Matrice des degrés
M= Matrice d'adjacence

Pour K4
D =

|2|0|0|0|
|-|
|0|3|0|0|
|0|0|3|0|
|0|0|0|2|
M =

| | | | |
|-|-|-|-|
|  0 |  1 |  1 | 0  |
| 1  |  0 | 1  | 1  |
| 1  | 1  | 0  |  1 |
| 0  |  1 | 1  | 0  |

L=

| 2  | -1  |-1   | 0  |
|----|-----|-----|----|
| -1 |  3  |  -1 | -1 |
| -1 | -1  |  3 | -1  |
|  0 |  -1 | -1  |  2 |
