# Mathématiques des signaux

## Rappels

Exemple: y''(t) = y'(t) + 6(t) = 12t + 20

Résolution classique en deux étapes
**a.** On considère une equation sans second membre
&emsp; y''(t) + y'(t) - 6y(t) = 0
On cherche la solution générale sous la forme
&emsp; y(t) = e^(rt)&emsp; r?
y'(t) = r.e^(rt) &emsp; y''(t) = r^2 e^(rt)
[ r² + r - 6 (e^(rt)) = 0 ]  <- r² + r - 6 = 0 est l'équation caracteristique

Delta = 1 + 24 = 25
x1 = -2
x2 = 2

La solution de l'equation sans secont membre est y(t) = A . e^(2t) + B . e^(-3t)
A et B dépendent de deux conditions initiales.

**b.** On considère l'équation avec second membre
On cherche une solution particulière
qui est particulièrement de la forme y(t) = at + b

y'(t) = a
y''(t) = 0
a - 6at - 6b = 12t + 20

a - 6b = 20
-6a = 12 => a = -2

6b = a - 20 = - 22
b = -(11/5)

Solution particulière de l'EASM
&emsp; y(t) = -2t - (11/5)

**c.** solution générale EASM = solution générale ESSM + solution particulière EASM
ce qui donne
[y(t) = A e^(2t) + B . e^(-2t) -2t - (11/5)]


## 2. Produit de convolution

x(t) et y(t)
x(t) * y(t) = Integrale(-INF,+INF, [x(T) * y(t - T).dT]) **T est un grand To**

* Commutativité x(t) * y(t) = y(t) * x(t)
* Associativité x(t) * [y(t) * z(t)] = [x(t) * y(t)] * z(t)
* Distributivité / assition x(t) * [y(t) + z(t)] = [x(t) * y(t)] + [x(t) * z(t)]
* Existe-t-il une **unité de convolution** u(t)
  - a.1 = 1.a = a [QQsoit] a
  - u(t) ? x(t) * u(t) = u(t) * x(t) = x(t) [QQsoit] x(t)

u(t) est le **pic de dirac** \delta(t)
![picdedirac](picdedirac.png)

## 3. Fonction complexe d'une variable complexe

Nombre complexe -> F(p) <- nombre complexe
p -F-> F(p)

## 4. Transformation de Laplace

F(p) = Integrale(0, +INF, [f(t) . e^(-pt) . dt])

p = nombre complexe
p = {sigma} + j{omega}

{omega} = pulsation rad/sec {omega} = 2Pi * f
f = fréquence (Hz)

La //FIXME le passage de l'espace temporel vers l'espace fréquentiel.

Condition d'existence de F(p)
Pout tous les signaux f(t) que l'ont peut observer, F() existe

Propriété:
* Linearité
* Théorème du retard
  - Signal court f(t) [nul, t <= 0]

L[f(t - T)] = e^(-Tp) * f(p)   __T est un grand To__

* Dérivation / Intégration
  - L[df(t) / dt] = pF(p) - f(t-0) = p.F(p)
    - C.I nulles -> Derrivation <=> Multiplication par p
    - Très facile de dériver et d'intégrer dans l'espace de Laplace
* Convolution
  - L[x(t) * y(y)] = X(p) * Y(p)
    - L[ \* ] = \*
    - Très facile de faire un produit de convolution dans l'espace de Laplace
* Théorème de **valeur initiale** / Théorème de la **valeur finale**
  - lim(t->0, [f(t)]) = lim(p->+INF, [p.F(p)])
  - lim(t->+INF, [f(t)] ) = lim(t->0, [p.F(p)]) -> Régime permanent en automatique

Les tableaux des 4 transformées de Laplace usuelles
