# Functionnal Programmation - 2018_02_05

* Yaka* en fonctionnel
* On va utiliser Lisp et Haskell
***
## Introduction

* Langage poreux
* Paradigme basé sur des trucs propres (lambda calcules?)

Pourquoi Haskell et Lisp?
* Deux langages: illustrer un paradigme independemment du langage de prog
* Deux langages très différents

* 1958 Premier dialecte de lisp McCarthy
  * Scheme
  * Comon Lisp
  * Clojure
  * emacslips

"Quoi faire plutot" que "comment faire"

Dans un langage imperatif, on parle d'instructions, en fonctionnel on parle d'expresisons

Se rapprocher le plus possible des mathématiques.

```common-lisp
(defun ssq(n)
  (if (= n 1 )
    1
    (+ (* n n) (ssq (1- n))))
```

Cette syntaxe est une S-Expr ``(fn x y z)``

```haskell
ssq :: Int -> Int
ssq 1 = 1
ssq n = n * n + ssq (n-1)
```

La fonction est un objet de premiere classe
Notion de Christopherr Strachey

Un langage sera fonctionnel si les fonctions seront d'ordre supérieur (comparable a des ints, float etc)
## Arguments fonctionnels
mapping: Traiter individuellement les éléments d'une liste par une fonction
folding: Comviner les éléments d'unel iste par une fonction

Fonctions anonymes
Utiliser les fonctions comme des objets dans les nommer, declarer

### Programmation fonctionnelle (im)pure

Pure: Pas d'effet de bord
Impure: avec effets de botd 
***
