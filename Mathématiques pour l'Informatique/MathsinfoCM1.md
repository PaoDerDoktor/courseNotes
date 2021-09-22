# Diagonalisation de matrices

## Matrices similaires

a) Soient `A` et `B` deux matrices ``n*n (n >= 1)``. Une matrice `A` est **similaire** à la matrice `B` si et seulement si il existe une matrice inversible `P` telle que :

```maths
B = P^(-1)AP
```

__Rappel__ : Une matrice `P` est inversible si il existe une matrice ``P^(-1) = P^(-1)P =I_n``

La relation de similarité est une relation d'équivalence (reflexive, symétrique et transitive).

Ainsi, l'ensemble des matrices similaires est formé de classes d'équivalence.

L'objectif est de trouver un "bon représentant" dans des classes.

Nous savons qu'à toute matrice carrée correspond un endomorphisme (respectant une application linéaire ``E --> E``). réciproquement, tout endomorphisme (``E --> E``) donne naissance à une matrice carrée `A` ``n*n``, `n` correspondant à ``dim(E)= n >=1``.

Ex. :
``B = {0, e_1, ..., e_n}``
``B' = f(B) = {e_1', ..., e_n'}``


La matrice ``P^(-1)AP`` est la matrice de la même transformation linéaire mais dans une autre base, qui est constituée de vecteurs de colonne P. Cela explique pourquoi beaucoup de propriétés de `A` et `B` sont les mêmes

b) Une matrice __est diagonalisable__ si elle est similaire à une matrice diagonale; i.e. ``P^(-1)AP=D`` avec`D` diagonale

__Propriété__ : Soient `A` et `B` deux matrices similaires, alors :
1. ``det(A) = det(B)``
2. `A` inversibles si et seulement si `B` inversible
3. `A` et `B` ont le même rang
4. `A` et `B` ont le même polynôme caractéristique.
5. `A` et `B` ont les mêmes valeurs propres

__Exemples de matrices similaires__

```maths
    +---     ---+        +---    ---+
    |  1     1  |        |  2    0  |
A = |           | et B = |          |
    | -2     4  |        |  0    3  |
    +---     ---+        +---    ---+
```

sont similaires car :

```maths
+---    ---+     +---    ---+ -1      +---     ---+         +---     ---+
|  2     1 |     |  1     1 |         |  1     1  |         |  1     1  |
|          |  =  |          |    x    |           |    x    |           |
|  0     4 |     |  1     2 |         | -2     4  |         |  1     2  |
+---    ---+     +---    ---+         +---     ---+         +---     ---+
      B             P^(-1)                  A                     P
```

Donc `A` est diagonalisable

__Remarques__ : Soit `A` une matrice n*n dans `R`, on peut lui associer l'endomorphisme ``R^n --> R^n``.

Définition par :

```f(x) = A x    | x \in R^n``

La matrice `A` peut être vue comme la matrice dune transformation linéaire, `P` peut être interprétée comme une matrice de changement de base.

c) Vecteurs propres, valeurs propres
- Un __vecteur propre__ pour une application linéaire est un vecteur __non nul__ tel que l'application linéaire `f` ne fait __que modifier sa taille__
- Une __valeur propre__ associée à un vecteur propre est le facteur qui modifie la taille propre
- Un __espace propre__ associé à une valeur propre est l'ensemble des vecteurs qui ont la même valeurs propres, plus le vecteur nul.

Par conséquent, si chercher les valeurs propres d'une matrice (respectant un endomorphisme) `A` n*n (resp. `f`), c'est résoudre le système linéaire suivant :

```maths
A.x = \lambda x    | x != 0
```

Soit ``I_n`` la matrice identité de rang `n`, alors :

```maths
Ax = \lambda x <==> Ax \lambda I_(n)x <==> (A - \lambda I_n) x = 0
```

C'est donc un système linéaire du type ``B . x = 0``. Un tel système a des solutions différentes de `0` (respectant ``x != 0``) si et seulement si `B` n'est pas __inversible__. Par conséquent, ``(A . \lambda I)x = 0`` a des solutions non triviales si et seulement si :

```maths
det(A - \lambda I) = 0
```

Cette équation s'appelle l'__équation caractéristique__. C'est un polynôme qui s'appelle __polynôme caractéristique__. Celui-ci est de degré `n` en `\lambda`, il possède `n` zéros réels ou complexes simple ou multiple.

__Exemple__ :

```maths
    +---     ---+
    |  1     2  |
A = |           |
    |  3     2  |
    +---     ---+
```

1) Calculer les valeurs propres :

```maths
                                (+---     ---+           +---     ---+)
                                (|  1     2  |           |  1     0  |)
det(A - \lambda I) = 0 <==> det (|           | - \lambda |           |) = 0 
                                (|  3     2  |           |  0     1  |)
                                (+---     ---+           +---     ---+)

                               (+---                     ---+)
                               (|  1-\lambda             2  |)
                       <==> det(|                           |) = 0
                               (|  3             2-\lambda  |)
                               (+---                     ---+)

                       <==> (1-\lambda)*(2-\lambda) - 6 = 0
                       <==> 2 - \lambda - 2 \lambda + \lambda^2 - 6 = 0
                       <==> \lambda^2 - 3*\lambda - 4 = 0
                         -> \delta = b^2 - 4ac = 9 - 4*(-4) = 9+16 = 25 = 5^2
                           --> \lambda_1 = (-b + \sqrt{\delta})/2a = (3+5)/(2*1) =  8/2 =  4
                           --> \lambda_2 = (-b - \sqrt{\delta})/2a = (3-5)/(2*1) = -2/2 = -2
```

Pour le vecteur propre :

```maths
(A - \lambda I) pour \lambda = \lambda_1 = 4 :
    ==> (A - 4*I) . x = 0

        (+---     ---+ -4  +---     ---+)   +--  --+   +- -+
        (|  1     2  |     |  1     0  |)   |  x_1 |   | 0 |
    ==> (|           |  *  |           |) * |      | = |   |
        (|  3     2  |     |  0     1  |)   |  x_2 |   | 0 |
        (+---     ---+     +---     ---+)   +--  --+   +- -+
    

    ==> {-3x_1 + 2x_2 = 0 
        { 3x_1 + 2x_2 = 0

    ==> 3x_1 = 2x_2    -> Je pose x_2 = t, alors x_y = (2/3)*t. Par conséquent tout vecteur
                          v_2 (t/(2/3)P) est vecteur propre associé à la valeur propre 4


(A - \lambda I) pour \lambda = \lambda_2 = -2 :
    ==> (A + 2*I) . x = 0

        (+---     ---+ 2   +---     ---+)   +--  --+   +- -+
        (|  1     2  |     |  1     0  |)   |  x_1 |   | 0 |
    ==> (|           |  *  |           |) * |      | = |   |
        (|  3     2  |     |  0     1  |)   |  x_2 |   | 0 |
        (+---     ---+     +---     ---+)   +--  --+   +- -+

```
<!--A COMPLETER POUR LAMBDA = -2 -->

```maths
D = P^(-1)AP

    +---     ---+
    |  4     0  |
D = |           |
    |  0    -1  |
    +---     ---+

      +--    --+          +- -+
      |    t   |          | t |
v_1 = |        |    v_2 = |   |
      | (2/3)P |          | t'|
      +--    --+          +- -+

en prenant t = 3 et t' = 1

    +---     ---+     +---     ---+   +---     ---+ -1
    |  2     1  |     |  4     0  |   | 2      1  |
P = |           |  *  |           | = |           |
    |  3    -1  |     |  0    -1  |   | 3     -1  |
    +---     ---+     +---     ---+   +---     ---+
```

d) Caractéristiques des matrices diagonalisables

__Théorème 1__ : Une matrice ``A*n`` est diagonalisable si et seulement si elle possède `n` vecteurs propres linéairement indépendants.

__Théorème 2__ : Les vecteurs propres correspondants à des caleurs propres distinctes sont linéairement indépendants.

__Théorème 3__ : Soit `E` un espace vectoriel et `A` une matrice dont les coefficients sont dans `E`, alors `A` est diagonalisable si et seulement si ``E = \sigma^(k)_(i=1) E_(\lambda_(i))`` où `\lambda` est valeur propre et où `\sigma` est somme directe des sous-espaces propres.

__Rappel__ : Soit E un espace vectoriel de dimension `n`. Soient `v_1`, `v_2`, `v_3`, ..., `v_k` `k` vecteurs de `E`, alors `v_1`, `v_2`, `v_3`, ..., `v_k` sont linéairement indépendants si et seulement si :

```maths

\sigma^(k)_(i=1) v_i = 0 <==> \alpha_1 = \alpha_2 = \alpha_3 = ... = \alpha_k = 0    pour \alpha dans C



                +-   -+            +-   -+
                | v_1 |            | w_1 |
                | v_2 |            | w_2 |
                | v_3 |            | w_3 |
\alpha . w <==> |  .  | = \alpha * |  .  | 
                |  .  |            |  .  |
                |  .  |            |  .  |
                | v_k |            | w_k |
                +-   -+            +-   -+
```

__Rappel__ : Calcul des déterminants

Pour un rang ``n = 2`` :

```maths
+-    -+
| a  b |
|      | = ad - bc
| b  c |
+-    -+
```

Pour un rang ``n >= 3`` :

On choisit une ligne ou une colonne et on développe à partir de cette ligne ou colonne. Ex :

```maths
+---   ---+       +--  --+     +--  --+     +--  --+
| a  b  c |       | e  t |     | d  t |     | d  e |
| d  e  f | = + a |      | - b |      | + c |      |
| g  h  i |       | h  i |     | g  i |     | g  h |
+---   ---+       +--  --+     +--  --+     +--  --+
```

On généralise dans le cas où ``n >= 4``.

__Exercice :__

```maths
         +---     ---+
         |  2  0  0  |
Soit A = |  1  2  1  |
         | -1  0  1  |
         +---     ---+
```

a) Trouver ses valeurs propres

```maths
                     +---                                 ---+                    (+--                  --+)
                     |  2-\lambda    0            0          |                    (| 2-\lambda  1         |)
det(A - \lambda*I) = |  1            2-\lambda    1          | = (2-\lambda) * det(|                      |) 
                     | -1            0            1-\lambda  |                    (| 0          1-\lambda |)
                     +---                                 ---+                    (+--                  --+)

                   = (2-\lambda) * ((2-\lambda)*(1-\lambda))
                   = (2-\lambda) * (2-2*\lambda-\lambda+\lambda^2)
                   = (2-\lambda) * (\lambda^2 - 3*\lambda + 2)
            ==> Selon la règle du produit nul, on a pour valeurs propres :
                   - \lambda_3 = 2
                   - Les solutions respectivement \lambda_1 et \lambda_2 de \lambda^2 - 3*\lambda + 2

            Solutions du polynôme :

    \delta = (-3)^2 - 4*1*2 = 9 - 8 = 1 ==> \delta > 0
        - \lambda_1 = (3-\sqrt(1))/2 = (3-1)/2 = 2/2 = 1
        - \lambda_2 = (3+\sqrt(1))/2 = (3+1)/2 = 4/2 = 2
```

Les valeurs propres sont ``\lambda_2 = \lambda_3 = 1`` et ``\lambda_1 = 2``

b) Trouver ses vecteurs propres

Pour `\lambda_2` = `\lambda_3` = 1 :

```maths
+---               ---+   +---         ---+
|  2-1    0      0    |   |  1    0    0  |
|  1      2-1    1    | = |  1    1    1  |
| -1      0      1-1  |   | -1    0    0  |
+---               ---+   +---         ---+

Système :

{  x_1              = 0
{  x_1 + x_2 + x_3  = 0
{ -x_1              = 0

{ x_1 = 0
{ x_2 = -x_3

On en déduit les vecteurs propres v_2, v_3 associés à \lambda_2, \lambda_3 = 1 du type :

    v = ( 0)
        ( t)
        (-t)
```

Pour `\lambda_1 = 2` :

```maths
+---               ---+   +---         ---+
|  2-2    0      0    |   |  0    0    0  |
|  1      2-2    1    | = |  1    0    1  |
| -1      0      1-2  |   | -1    0   -1  |
+---               ---+   +---         ---+

Système :

{ x_1 = x_3

On en déduit le vecteur propre v_1 associé à \lambda_1 = 2 du type :

    v = ( t)
        ( u)
        (-t)
```

<!-- Colo des parenthèses : }}}}}}-->

c) Conclure (diagonalisable ou pas ?)

On sait qu'une matrice `A` est diagonalisable si tous ses vecteurs propres sont linéairement indépendants. On cherche donc 3 vecteurs linéairement indépendants, associé à chaque vecteur propre de `A`.

On a deux valeurs confondues, alors on se limite à deux vecteurs :

```maths

      ( 1 )        ( 0 )   (0)
\alpha( 0 ) + \beta( 1 ) = (0) <==> { \alpha * 0 + \beta * 1 = 0  ==> \alpha = 0 & \beta = 0
      (-1 )        ( 0 )   (0)      { \alpha * 1 + \beta * 0 = 0
```

On a nos deux vecteurs linéairement indépendants, donc `A` est bien diagonalisable. Soit ``D = P^(-1)AP`` :

```maths
    +--   --+        +---       ---+
    | 1 0 0 |        |  0   1   0  |
D = | 0 2 0 | et P = |  1   0   1  |
    | 0 0 2 |        | -1  -1   1  |
    +--   --+        +---       ---+
```

## Matrices orthogonales

### Définition

Soit `A` une matrice ``m*n``, elle est orthogonale si et seulement si ``A^(T)A = AA^(T) == I`` avec ``A^T`` la transposée de `A`

#### Rappel

Soit `A` une matrice ``n*m``, sa transposée ``A^(T)`` est la matrice dont les lignes de ``A`` deviennent les colonnes.

### Suite de la définition

Comme ``A^(-1)A = AA^(-1) = I <==> A^(-1) = A^(T)``, si `A` est orthogonale, ``det(A^(-1)A) = det(I) = 1``.Donc, ``det(A^(T)A) = det(A^T)*det(A) = 1 ===> det(A) = +/- 1`` car ``det(A) = det(A^T)``

- Si ``det(A) =  1`` alors `A` est une matrice de rotation
- Si ``det(A) = -1`` alors `A` est une matrice de rotation suivie d'une symétrie

Une matrice `A` ``m*n`` est orthogonalement diagonalisable s'il existe une matrice `P` orthogonale telle que ``P^(T)AP = D`` avec ``P^(T)P = I = PP^(T)`` et `D` matrice diagonale.

### Théorème

Soit `A` une matrice ``m*n``, les affirmations suivantes sont équivalentes :
- `A` est orthogonalement diagonalisable
- `A` est symétrique (``A^(T) = A``)

### Proposition

Toute matrice symétrique `A` ``n*n`` a ses valeurs propres valeurs propres **réelles**

### Proposition

Soit une matrice ``n*n`` symétrique `A`.
Soient ``\lambda_1``, ``\lambda_2`` deux valeurs propres distinctes et ``x_1``, ``x_2`` deux vecteurs propres associés à ``\lambda_1`` et ``\lambda_2`` respectivement alors ``x_1 \perpendiculaire x_2`` (i.e. ``x_1``, ``x_2`` sont orthogonaux).

### Exercice

```maths
    +---       ---+
    |  2   1   0  |
A = |  1   1   1  |
    |  0   1   2  |
    +---       ---+
```

a) Trouver les valeurs propres

```maths
                          (+---                   ---+)      (+---           ---+)
                          (|  1-\lambda   1          |)      (|  1   1          |)
det(A) = (2-\lambda) * det(|                         |) - det(|                 |)
                          (|  1           2-\lambda  |)      (|  0   2-\lambda  |)
                          (+---                   ---+)      (+---           ---+)

        = (2-\lambda) * ((1-\lambda)*(2-\lambda)) - 2 + \lambda
        = (2-\lambda) * ((1-\lambda)*(2-\lambda) + 1)
        = (2-\lambda) * (2 - \lambda - 2*\lambda + \lambda^2 + 1)
        = (2-\lambda) * (3 - 3*\lambda + \lambda^2)

        On a plusieurs valeurs propres :
            - \lambda_3 = 2
            - \lambda_1 et \lambda_2 les solutions de \lambda^2 - 3*\lambda + 3

        Étude de \lambda^2 - 3*\lambda + 3:

        \delta = (-3)^2 - 4*1*3 = 9 - 12= -
