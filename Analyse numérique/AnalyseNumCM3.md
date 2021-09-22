# Analyse numérique, CM/TD 3

## Exercice sur les précédents CMs

On a :
```maths
f : R^2 - {(0, 0)} --> R
        (x_1, x_2) --> ln(x_(1)^2 + x_(2)^2)
```

D'ici, calculer ``\grad f(x)``  et ``\delta f(x)``

__Calcul de ``\grad f(x)`` :__

```maths
             +---                          ---+   +---                          ---+
             |  (\drond f(x)) / (\drond x_1)  |   |  (2x_1) / (x_(1)^2 + x_(2)^2)  |
\grad f(x) = |                                | = |                                |
             |  (\drond f(x)) / (\drond x_2)  |   |  (2x_2) / (x_(1)^2 + x_(2)^2)  |
             +---                          ---+   +---                          ---+


(\drond^2 f(x)) / (\drond x_(1)^2) = (2 * (x_(1)^2 + x_(2)^2) - 2 * x_1 * (2*x_1)) / (x_(1)^2 + x_(2)^2)
                                   = (-2*x_(1)^2 + 2*x_(2)^2) / (x_(1)^2 + x_(2)^2)^2

(\drond^2 f(x)) / (\drond x_(2)^2) = A COMPLETER

\delta f(x) = ((\drond^2 f(x)) / (\drond x_(1)^2)) + ((\drond^2 f(x))/ (\drond x_(2)^2)) = 0
```

## Chapitre 2 : Approximation par différences finies pour les problèmes elliptiques

``\omega \includes R^n    f : \omega --> R`` une fonction régulière

On cherche une solution de problème elliptique suivant :

(1)
```maths
{ -\delta u(x) = \sigma_(i=1)^(n) (\drond^2 u(x))/(\drond x_(i)^2) = f(x), x \in R
{ u(x) = 0 sur \drond R
```

<!-- Pour la colorisation des parenthèses : }} -->
Pour ``n=1`` : ``\omega`` sur un intervalle ``]0, 1[`` :
<!-- Pour la colorisation des parenthèses : ] -->

(2)
```maths
{ - u''(x) = f(x)
{ u(0)= u(1) = 0
```
<!-- Pour la colorisation des parenthèses : }} -->

(1) et (2) sont des __problèmes continus__.

__**On cherche des solutions *approchées* de `(1)` et `(2)`**__

Donc, on cherche une approximation de ``u'`` et de ``u''``.

### Formule de Taylor

On note ``f^n`` la dérivée ``n`` fois de ``f`` (*exemple :* ``f^2`` est la dérivée seconde). C'est la dérivée à l'ordre `n` de `f`.

On pose :

```maths
n \in N
f \in C^(n)([a, b])
f^(n+1) existe
```

Alors il existe ```o \in ]a, b[ tel que:
<!-- Pour la colorisation des parenthèses : ] -->

```maths
          n    (b-a)^k             (b-a)^(n+1)
f(b) = \sigma  -------  f^(k)(a) + ----------- f^(n+1)(o)
         k=0      k!                  (n+1)!

       \_______________________/   \____________________/
                  |                          |
              Polynôme                     Reste
```

Sur ``[0, x]`` :

```maths
f(x) = f(0) + f'(0)*x + (1/2)*f''(0)*x^2 + ... + 1/(n!)*f^(n)(0)*x^n + reste
```

On remarque que ``f(x)`` est ici une fonction composée d'un polynôme (ensuite noté ``P(n)``) et d'un reste. On note donc :

```maths
f(x) = P_(n)(x) + Reste(x) ====> f(x) ~= P_(n)(x)
```

Sur ``[x, x+(h/2)]`` à l'ordre `?`, ``n=1`` :

```maths
u(x+(h/2)) = u(x) + (h/2)*u'(x) + O(h^2)
```

Sur ``[x-(h/2), x]`` à l'ordre `1`, ``n=1`` :

```maths
u(x-(h/2)) = u(x) - (h/2)*u'(x) + O(h^2)
```

```maths
= u(x + (h/2)) - u(x - (h/2)) ~= hu'(x) + O(h^2)

u'(x) ~= (u(x+(h/2)) - u(x-(h/2))) / h
```

> NOTE : non, je sais pas du tout ce que `h` représente... Peut être un "indice de précision" ?
> > Yup, ça a l'air d'être ça vu ce qui arrive ensuite

### Retour à l'exemple principal

On applique ``(3)`` (?????) à ``u'`` :

```maths
u''(x) = (u'(x+(h/2)) - u'(x-(h/2))) / h

u'(x+(h/2)) = (u(x+h) - u(x)) / h

u'(x-(h/2)) = (u(x) - u(x-h)) / h



          u(x+h) - u(x)   u(x) - u(x-h)
          ------------- - -------------
                h               h              u(x+h) - 2u(x) + u(x-h)
u''(x) = -------------------------------- ~= ---------------------------
                        h                                h^2
```

```maths
Schéma :

                      h
                  <------->
       |         |         |
-------+---------+---------+------
       |         |         |
      x-h        x        x+h
```

### Discrétisation uniforme de [0, 1]

On prends l'intervalle [0, 1], et on le discrétise en `n` parts égales selon un écart `h`.

Schéma :
```maths
                            h
                         <----->
|       |       |       |       |       |       |       |
+-------+-------+-------+-------+-------+-------+-------+
|       |       |       |       |       |       |       |
0             x_i-1    x_i    x_i+1                     1
```

On a donc :
```maths
                                           ----------+
             u(x_(i+1)) - 2u(x_i) + u(x_(i-1))       |
u''(x_i) = -------------------------------------     |
                            h^2                      |    approximation
                                                     |--> par différences
             u(x_(i+1)) - u(x_(i-1))                 |    finies centrées
u'(x_i)  = ---------------------------               |
                       2*h                           |
                                           ----------+

             u(x+i) - u(x_i)                 u(x_i) - u(x_i+1)
u'(x_i) ~= -------------------, u'(x_i) ~= --------------------
                    h                                h
```

### Images et coordonnées

On peut donner des coordonnées d'une image en deux dimensions sur ``R^2``

```maths

           y ^
             |
             |
             |
             +-+-+-+-+-+-+ ^
             | | | | | | | | h_y
             +-+-+-+-+-+-+ v
             | | | | | | |
         j+1 +-+-+-+-+-+-+
             | | | | | | |
           j +-+-+-O-+-+-+
             | | | | | | |
         j-1 +-+-+-+-+-+-+
             | | | | | | |         x
-+-+-+-+-+-+-+-+-+-+-+-+-+-------->
             |   i i i <->
             |   -   + h_x
             |   1   1
             |
             |   
```

Le point `O` sur le schéma vaut ``u(x_i, y_j)``

__Donner une approximation de ``\grad u(x_i, y_j)`` et ``\delta u(x_i, y_j)``

```maths
\grad u(x_i, y_j):


  \drond u(x_i, y_j)        u(x_(i-1), y_j) - u(x_(i+1), y_j)
---------------------- ~= ------------------------------------- 
        \drond x                           2h_x

  \drond u(x_i, y_j)        u(x_i, y_(j-1)) - u(x_i, y_(j+1))
---------------------- ~= -------------------------------------
        \drond y                           2h_y


\delta u(x_i, y_j) :


  \drond^2 u(x_i, y_j)       u(x_(i+1), y_j) - 2u(x_i, y_j) + u(x_(i-1), y_j)
------------------------ = ----------------------------------------------------
      \drond x^2                                  (h_x)^2


  \drond^2 u(x_i, y_j)       u(x_i, y_(j+1)) - 2u(x_i, y_j) + u(x_i, y_(j-1))
------------------------ = ----------------------------------------------------
      \drond y^2                                  (h_y)^2
```

#### Exemple

On pose :

```maths
h_x = 1/5
h_y = 1/6
I(i, j)

0 <= i <= 5
0 <= j <= 6
```

L'image représentée :

```
  +----                      ----+   
  |  20    20    20    20    20  |
  |  20    20    20    20    20  |
  | 180   180  *180*   50    50  |
  |   x     x     x     x     x  |
  |   x     x     x     x     x  |
  |   x     x     x     x     x  |
0 +----                      ----+
  0
```

__Calculer les approximations par différences finies de ``\grad I(3, 4)`` et ``\delta I(3, 4)`` :__

Calcul du gradient :

```maths
                +----                  ----+   +----       ----+   +--    --+
                |  (50 - 180) / (2*(1/3))  |   | -130 / (2/3)  |   |  -195  |
\grad I(3, 4) = |                          | = |               | = |        |
                |   (20 - 180) / (2*1/6)   |   | -160 / (1/3)  |   |  -480  |
                +----                  ----+   +----       ----+   +--    --+


                   50 - 2*180 + 180       20 - 2*180 + 180      -130      -160
\delta I(3, 4) = -------------------- + -------------------- = ------- + ------
                         (1/5)^2               (1/6)^2           1/25     1/36
```
<!-- A VERIFIER -->

On rappelle le problème (2) : 

```maths
{ - u''(x) = f(x)    (sur ]0, 1[)
{ u(0)= u(1) = 0
```
<!-- Pour la colorisation des parenthèses : }]} -->

On schématise l'intervalle :
```math
                           h
                        <----->
|     |     |     |     |     |     |     |     |     |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+
|     |     |     |     |     |     |     |     |     |
0                j-1    j    j+1                      1
```

Avec `n`, le nombre de partitions, fixé avec ``h= 1/(n+1)``.

Prenons ``x_(j)^n = jh``, avec ``0 <= j < n``.

```maths
u(x) ~= U = (U_(1)^n, U_(2)^n, ..., U_(n)^n) vecteur approchant ``u(x)``
```

Le Problème approché de ``(1)``, noté ``(4)`` :

(4)
```maths
{ - (U_(j+1)^n + 2*U_(j)^n + U_(j-1)^n) / (h^2) = f(x_(j)^n) avec 0 <= j <= n
{                           U_(0)^n = U_(n+1)^n = 0


{ - (U_(2)^n + 2U_(1) + 0)         / (h^2) = f(x_(1)^n) = F_(1)^n
{ - (U_(3)^n + 2U_(2)^n - U_(1)^n) / (h^2) = f(x_(2)^n) = F_(2)^n
{                                          .
{                                          .
{                                          .
{- (0 - 2U_(n)^n + U_(n-1)n)       / (h^2) = f(x_(n)^n) = F_(n)^n
```
<!-- Pour la colorisation des parenthèses : }}}}}}}} -->

On peut écrire ce système sous forme matricielle :
```maths
+----                        ----+   +----   ----+   +----   ----+
|  2   -1    0    ...    0    0  |   |  U_(1)^n  |   |  F_(1)^n  |
| -1    2   -1    ...    0    0  |   |  U_(2)^n  |   |  F_(2)^n  |
|  0    .                     .  |   |     .     |   |     .     |
|  .         .                .  | * |     .     | = |     .     |
|  .               .          .  |   |     .     |   |     .     |
|  .                     .   -1  |   |     .     |   |     .     |
|  0                    -1    2  |   |  U_(n)^n  |   |  F_(n)^n  |
+----                        ----+   +----   ----+   +----   ----+

A^n * U^n = F^n
```

Cette matrice est définie positive.