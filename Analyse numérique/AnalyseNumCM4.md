# Analyse numérique, CM/TD 4

## Exercice sur les précédentes séances

On pose :

```maths
u : R*R_+ ------> R
   (x, t) ------> u(x, t)
```

Soient ``\delta x, \grad > 0``, on considère les points ``x_k = k \delta x`` et ``t_n = n \delta t``, ``k = 0, 1, 2, ...``

Schématisation :
```maths
               ^
               |
              -+-
               |
        y_t+1 -+-
               |
          y_t -+-
               |
        y_t-1 -+-
               |
              -+-
               |
              -+-
|    |    |    |    |    |    |    |    |    |    |    |
+----+----+----+----+----+----+----+----+----+----+----+-->
|    |    |    |    |    |    |    |    |    |    |    |
              -+-              x_k-1  |  x_k+1
               |                     x_k
              -+-
               |
              -+-
               |
```

### 1) Déterminer un schéma de différences finies pour :

```maths
  \drond u(x, t)           \drond u(x, t)
------------------ + a * ------------------ = 0
     \drond t                 \drond x
```
Avec ``a > 0``


--> On pose

```maths
  \drond u(x, t)        u(x_k, t_(n+1)) - u(x_k, t_(n-1))        U_(k)^(n+1) - U_(k)^(n-1)
------------------ ~= ------------------------------------- ~= -----------------------------
     \drond t                     2 * (\delta t)                        2 (\delta t)



  \drond u(x, t)        U_(k)^(n+1) - U_(k)^(n)
------------------ ~= ---------------------------
     \drond t                  \delta t          

  \drond u(x, t)        U_(k)^(n) - U_(k)^(n-1)
------------------ ~= ---------------------------
     \drond t                  \delta t



  \drond u(x, t)        U_(k+1)^(n) - U_(k-1)^(n)
------------------ ~= -----------------------------
     \drond x                 2(\delta x)           

  \drond u(x, t)        U_(k+1)^(n) - U_(k)^(n)
------------------ ~= ---------------------------
     \drond x                  \delta x

  \drond u(x, t)        U_(k)^(n) - U_(k-1)^(n)
------------------ ~= ---------------------------
     \drond x                  \delta x



  \drond u(x, t)           \drond u(x, t)        U_(k)^(n+1) - U_(k)^(n)           U_(k+1)^(n) - U_(k)^(n)
------------------ + a * ------------------ ~= --------------------------- + a * ---------------------------
     \drond t                 \drond x                  \delta t                          \delta x




                                \delta t
U_(k)^(n+1) - U_(k)^(n) + a * ------------ * (U_(k+1)^n - U_(k)^(n)) = 0
                                \delta x

                                \delta t
U_(k)^(n+1) = U_(k)^(n) - a * ------------ * (U_(k+1)^n - U_(k)^(n))
                                \delta x
```

On retiens le schéma sous sa dernière forme, plus pratique
<!-- NOTE : wtf ? -->

On le pose ainsi :

```maths
\delta x = 1/N

                      \delta t                            \delta t
U_(k)^(n+1) = - a * ------------ U_(k+1)^(n) + (1 + a * ------------) U_(k)^n        | k = 1, 2, ... N
                      \delta x                            \delta x

            = \sigma_(l=1)^(N) \Q_(k, l) U_(l)^(N)

U^(n+1) = Q U^n
```

Avec `Q` la matrice bidiagonale suivante :

```maths
+----
|             \delta t                 \delta t
|   n + a * ------------       - a * ------------
|             \delta x                 \delta x
|
| 
|                       0        n + a * --------
|
|
|                       0
|
|
|                       .
|                       .
|                       .
|
|
|                       0
|
+----
```
<!-- A compléter, j'ai pris la photo, il s'est trompé de tableau à effacer mais il s'en est rendu compte XD -->

## Visiblement on est passés à autre chose, je bite rien à son organisation


On a le problème continu suivant :
```
{ - u''(x) = f(x) dans ]0, 1[
{ u(0) = u(1) = 0
```

<!-- NOTE : pour la colorisation des parenthèses : }]} -->

On cherche l'approximation de u''

On schématise :

```maths
                           h
                        <----->
|     |     |     |     |     |     |     |     |     |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+
|     |     |     |     |     |     |     |     |     |
0              x_(i-1)  x  x_(i+1)
```

On a donc :
```maths
           u(x_(i+1)) - 2 u(x_i) + u(x_(i-1))
u''(x) = --------------------------------------
                          h^2
```

On pose alors
```maths
n = 2
\omega rectangle sur l'image
\omega = ]0, 1[ * ]0, 1[

                        ^ y
                        |
                       -+-
                        |
               y_(j+1) -+- ^
                        |  | h_y
                   y_j -+- v
                        |
               y_(j-1) -+-
                        |
                       -+-
                        |
                       -+-
                        |                         h_x
                       -+-                      <----->
|     |     |     |     |     |     |     |     |     |     |     |
+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----+-----> x
|     |     |     |     |     |     |     |     |     |     |     |
                       -+-             x_(i-1)  x   x_(i+1)
                        |
                       -+-
                        |
                       -+-
                        |

    /                         \drond^2 u(x, y)       \drond^2 u(x, y)
   /   - \delta u(x, y) = - -------------------- - -------------------- = f(x, y) dans \omega
  |                             \drond^2 x^2            \drond y^2
 <
  |
   \   u(x, y) = 0 sur \drond R
    \
```

On cherche une approximation ``U_(ij)`` de ``u(x_i, y_i)``.

```mahs
    \drond^2 u(x_i, y_j)        - u(x_(i+1), y_j) + 2u(x_i, y_j) - u(x_(i-1), y_j)
- ------------------------ ~= ------------------------------------------------------
         \drond x^2                                 (h_x)^2

    \drond^2 u(x_i, y_j)        - u(x_i, y_(j+1)) + 2u(x_i, y_j) - u(x_i, y_(j-1))
- ------------------------ ~= ------------------------------------------------------
         \drond y^2                                 (h_y)^2
```

D'où le schéma numérique suivant :

```maths
u(x_i, y_j) = U_(ij)

    /   2U_(ij) - U_(i+1, j) - U_(i-1, j)       2U_(ij) - U_(i,j+1) - U_(i, j-1)
   /  ------------------------------------- + ------------------------------------ = F_(ij) = f(x_i, y_j)
  |                  (h_y)^2                                (h_x)^2
 <
  |   U_(0, j) = U_(N+1, j) = 0
   \ 
    \ U_(i, 0) = U_(u, M+1) = 0
```

Avec ``1 <= i <= N``, ``1 <= j <= M``

La matrice U (pas à apprendre) est tridiagonale par bloc :

```maths
    +-- --+         +---    ---+       +-- --+         +---    ---+
    | U_1 |         | U_(2, j) |       | F_1 |         | F_(1, j) |
    | U_2 |         | U_(1, j) |       | F_2 |         | F_(2, j) |
    |  .  |         |     .    |       |  .  |         |     .    |
U = |  .  |   U_j = |     .    |   F = |  .  |   F_j = |     .    |
    |  .  |         |     .    |       |  .  |         |     .    |
    | U_M |         | U_(N, j) |       | F_M |         | F_(M, j) |
    +-- --+         +---    ---+       +-- --+         +---    ---+


    +-----              ----+
    | B   C   0   .   .   0 |
    | C   B   C             |
A = | 0   C   .   .         |
    | .       .   .   .     |
    | .           .   .   C |
    | 0               C   B |
    +----               ----+
```

## Les différences finies pour l'équation de la chaleur en dimension `1`

On commence par un exercice afin de montrer l'idée.

### Exercice d'exemple

On pose ``\omega = ]0, 1[``.

```maths
      /   \drond u(x, t)      \drond^2 u(x, t')
     /  ----------------- - --------------------- = 0      | x \in \omega, t > 0
(P) <        \drond t            \drond x^2
     \
      \ u(x, 0) = u^0(x)      | x \in \omega
```

On introduit le pas de temps ``\delta t``, et le pas d'espace ``\delta x``

On cherche une approximation ``(U_i)^n`` en ``x_i = i \delta x`` et en ``t = n \delta t``.

__**Question :**__ *Donner un schéma par différences finies pour résoudre ``(P)``

```maths
  \drond u(x, t)        u(x_i, t_(n+1)) - u(x_i, t_(n-1))
------------------ ~= -------------------------------------
     \drond t                     2 * \delta t

                        (U_i)^(n+1) - (U_i)^n
                   ~= -------------------------
                              \delta t

  \drond^2 u(x, t)        (U_(i+1))^n - 2(U_i)^n + (U_(i-1))^n
-------------------- ~= ----------------------------------------
    \drond x^2                       (\delta t)^2


  \delta u(x, t)       (U_i)^(n+1) - (U_i)^n
------------------ - -------------------------
     \delta t              (\delta x)^2        
```

<!-- A COMPLETER -->