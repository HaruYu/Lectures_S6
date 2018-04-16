---
author: trinh_v
title: Compression
...

# Introduction to Data Compression

* Guillaume Tochon

* [lien](www.lrde.epita.fr/~gtochon/CODO/)
* Partiels: DST de 2h -en partie QCM et en partie questions ouvertes-

## Definitions

A file has a size on a storing media. The aim is to encode this file to get it smaller.
Data decompression is the inverse process, restoring back to the original form.

## Reasons to use it

Example: an HD movie weighs:

- A color is 1 byte
- A pixel is 3 bytes (RGB)
- 1280 * 720 pixels on the screen
- 25FPS
- 1h30 long

$\rightarrow$ 373Go (80 DVDs) excluding the sound

* Save space and Memory
* Speed up processing time
* Increase compatibility (NIKON & Canon for Example)
* Increase security: compress is to encrypt.

## History

1948 : Claude Shannon.

# Data compression

Two types of compression :

* Lossless compresson
* Lossy compression

What informations can we loss if this is a lossy one?

## Losy compression

* The user doesn't have to notice the difference between the Raw end the compressed file

***

# A flavor of Information theory

What kind of information can pe compressed?

* Redundancy
* Wastes 32 gray levels, do we really need 1byte to encode it? No.

Information theory provies the etropy the tool we need to qualify compressbility
 of a given file

A totally random file cannot be compressible. Where as an ordonned one can be
 compressed.

## Information definition (Shannon's definition)

"This year, Christmas will be celebrated on December the 25th." This is not an
information.

"This year, it will be 15°C on average on Bastille day." This sentence has a little
information.

"Next year, PSG will win the UEFA Champions league." Maximum information. (trolled
by Tochon, GG)

> q(m) = f(1/p(m))

## Introduction to entropy

Alphabet $\Sigma$ composé de $N_\Sigma$ symboles,

$\Sigma = (s_1, s_2, s_3, ..., s_{\Sigma_n})$ avec leur probabilité d'occurence $p = p(s_i)
= probabilité d'occurence du symbole s_i$

F fichier de sigma contenant $N_f$ symboles de $\Sigma$ statistiquement, $s_i$ est présent
$N_f * p_i$ fois.

Symbole $s_i \rightarrow q(s_i) = -log_2(p_i)$

$\rightarrow$ quantité d'informations totale de $s_i$ dans F

$Q_{tot}(s_i) = -N_p p_i log_2(p_i)$

F est composé de $s_1, s_2,... , s_{n_\Sigma}$

$Q_{tot}(F) = Q_{tot}(s1) + Q_{tot}(s2)+.... = \Sigma_{i = 1}^{N_2} -N_F p_i log_2(p_i)$

Entropie = $Q_tot(p) / N_f = H$

Unités: $Q_{tot}$ = Sh

H = Sh/symbole

H ne dépend pas du fichier F -> H ne dépend que de l'alphabete considéré est de la distribution de probabilité des symboles qui le composent.

X une variable aléatoire

$$ X = {x, ..., x_n} p_i = proba(X = x_i)$$
$$ E[X] = \Sigma_{i = 1}^{N}xp = \Sigma_{i=1}^n x proba(X = x_i)$$
$$ E[\phi(x)] = \Sigma_{i = 1}^N \phi(x_i)p_i = \Sigma_{i = 1}^N -log_2(p_i)p_i$$
$$ = \Sigma_{i = 1}^N q(s_i)p_i = E[q(s_i)]$$

$$ v_\Sigma = {0, 1} p(0) = p_0 = p$$
$$ p(1) = p_1  = 1-p $$
$$ H = -p log_2(p) - (1 - p)log_2(1-p) = H(p)$$

## Exercise

> How many bits are necessary to encode the file F = {ACABBDDBAAABCAAA} uncompressed?
> Assuming that the probability of occurence of the symbols in F is equal to their
> relative frequency, what would be the smallest compressed size of the file F?


* 8/16 pour A -> 1/2
* 4/16 pour B -> 1/4
* 2/16 pour C -> 1/8
* 2/16 pour D -> 1/8

Au minimum 2 bits pour encoder 4 caractères. Donc au maximum 32 bits pour ce text.

Calcul de l'entropie

$$ H(A) = -8/16 * \log_2(8/16) = 0.5 $$
$$ H(B) = 0.5 $$
$$ H(C) = 0.375 $$
$$ H(D) = 0.375 $$
$$ H = 1.75 = 7/4 Sh/symb $$
